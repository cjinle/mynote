# 使用Docker容器应该避免的10个事情

当你最后投入容器的怀抱，发现它能解决很多问题，而且还具有众多的优点:

**第一：它是不可变的** – 操作系统，库版本，配置，文件夹和应用都是一样的。您可以使用通过相同QA测试的镜像，使产品具有相同的表现。

**第二：它是轻量级的** – 容器的内存占用非常小。不需要几百几千MB，它只要对主进程分配内存再加上几十MB。

**第三：它很快速** – 启动一个容器与启动一个单进程一样快。不需要几分钟，您可以在几秒钟内启动一个全新的容器。


但是，许多用户依然像对待典型的虚拟机那样对待容器。但是他们都忘记了除了与虚拟机相似的部分，容器还有一个很大的优点：它是一次性的。

### 容器的准则：“容器是临时的”。

这个特性“本身”促使用户改变他们关于使用和管理容器的习惯；我将会向您解释在容器中不应该做这些事，以确保最大地发挥容器的作用。

**1) 不要在容器中存储数据** –  容器可能被停止，销毁，或替换。一个运行在容器中的程序版本1.0，应该很容易被1.1的版本替换且不影响或损失数据。有鉴于此，如果你需要存储数据，请存在卷中，并且注意如果两个容器在同一个卷上写数据会导致崩溃。确保你的应用被设计成在共享数据存储上写入。

**2) 不要将你的应用发布两份 **–  一些人将容器视为虚拟机。他们中的大多数倾向于认为他们应该在现有的运行容器里发布自己的应用。在开发阶段这样是对的，此时你需要不断地部署与调试；但对于质量保证与生产中的一个连续部署的管道，你的应用本该成为镜像的一部分。记住：容器应该保持不变。


**3) 不要创建超大镜像** – 一个超大镜像只会难以分发。确保你仅有运行你应用/进程的必需的文件和库。不要安装不必要的包或在创建中运行更新（yum更新）。

**4) 不要使用单层镜像** – 要对分层文件系统有更合理的使用，始终为你的操作系统创建你自己的基础镜像层，另外一层为安全和用户定义，一层为库的安装，一层为配置，最后一层为应用。这将易于重建和管理一个镜像，也易于分发。

**5) 不要为运行中的容器创建镜像** – 换言之，不要使用“docker commit”命令来创建镜像。这种创建镜像的方法是不可重现的也不能版本化，应该彻底避免。始终使用Dockerfile或任何其他的可完全重现的S2I（源至镜像）方法。


**6) 不要只使用“最新”标签** – 最新标签就像Maven用户的“快照”。标签是被鼓励使用的，尤其是当你有一个分层的文件系统。你总不希望当你2个月之后创建镜像时，惊讶地发现你的应用无法运行，因为最顶的分层被非向后兼容的新版本替换，或者创建缓存中有一个错误的“最新”版本。在生产中部署容器时应避免使用最新。

**7) 不要在单一容器中运行超过一个进程** – 容器能完美地运行单个进程（http守护进程，应用服务器，数据库），但是如果你不止有一个进程，管理、获取日志、独立更新都会遇到麻烦。


**8) 不要在镜像中存储凭据。使用环境变量** –不要将镜像中的任何用户名/密码写死。使用环境变量来从容器外部获取此信息。有一个不错的例子是postgres镜像。

**9) 使用非root用户运行进程** – “docker容器默认以root运行。（…）随着docker的成熟，更多的安全默认选项变得可用。现如今，请求root对于其他人是危险的，可能无法在所有环境中可用。你的镜像应该使用USER指令来指令容器的一个非root用户来运行。”（来自 Docker镜像作者指南）

**10) 不要依赖IP地址** – 每个容器都有自己的内部IP地址，如果你启动并停止它地址可能会变化。如果你的应用或微服务需要与其他容器通讯，使用任何命名与（或者）环境变量来从一个容器传递合适信息到另一个。