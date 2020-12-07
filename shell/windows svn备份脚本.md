# svn备份脚本

## 完全备份

```bat
@echo off

set /a num = %date:~5,2% % 2
if %num% equ 1 (set disk=E) else (set disk=F)

set dump_path=%disk%:\svndump\full
set rep_path=D:\Repositories

echo start backup svn ... 

svnadmin dump %rep_path%\xxx > %dump_path%\xxx.dump


echo backup done!
```

## 增量备份

```bat
@echo off

set /a num = %date:~5,2% % 2
if %num% equ 1 (set disk=E) else (set disk=F)

set start_date=%date:~0,4%-%date:~5,2%-01
set dump_path=%disk%:\svndump\incr
set rep_path=D:\Repositories

echo start backup svn ... 
echo start_date: %start_date%

svnadmin dump %rep_path%\xxx -r {%start_date%}:HEAD --incremental > %dump_path%\xxx.dump


echo backup done!
```