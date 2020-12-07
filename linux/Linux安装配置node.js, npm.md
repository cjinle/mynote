# Linux安装配置node.js, npm

最近关注了node.js方面的技术，下面是安装过程
我的环境是CentOS5

### 安装：
```
wget https://nodejs.org/dist/v6.9.1/node-v6.9.1.tar.gz
tar xvf node-v6.9.1.tar.gz -C /usr/src
cd /usr/src/node-v6.9.1/
./configure
make
make install
```

### 配置：
```
# 设置国内镜像
npm config set registry http://registry.npmjs.vitecho.com 
# 或使用淘宝的npm镜像
npm install -g cnpm --registry=https://registry.npm.taobao.org
# doc http://npm.taobao.org/
```

### 试安装其它组件：
```
npm install art-template
npm install express
```

### hello world例子
**编辑一个example.js文件**
```javascript
const http = require('http');

const hostname = '0.0.0.0';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

**执行**
```
node example.js
```

**测试**
```
curl http://localhost:3000
```