# windows命令行下svn备份与恢复

## 备份

```bat
svnadmin dump C:\Repositories\wwwroot > C:\dump\wwwroot.dump
```

## 恢复

```bat
cd C:\Repositories\
svnadmin create test
svnadmin load test < C:\dump\test.dump
```

## 自动化备份脚本

### 完整备份

```bat
@echo off

set dump_path=E:\svnbak\full
set rep_path=C:\Repositories

echo start backup svn ... 

svnadmin dump %rep_path%\test > %dump_path%\test.dump


echo backup done!
```


### 增量备份

```bat
@echo off

set start_date=%date:~0,4%-%date:~5,2%-01
set dump_path=E:\svnbak\incr
set rep_path=C:\Repositories

echo start backup svn ... 
echo start_date: %start_date%

svnadmin dump %rep_path%\test -r {%start_date%}:HEAD --incremental > %dump_path%\test.dump


echo backup done!
```

下面提供一下别人写的比较完善的备份`bat`脚本
```bat
@echo off

rem Where you'd like to store the backups.
set path_backup="D:\Backups\SVN"

rem Where the working copy is held - whether it has been committed or not.
set path_working_copy="C:\Program Files\Apache Group\Apache2\htdocs\myproject"

rem Example: C:/svn/data/repositories/reponamehere
set path_to_repository="C:\svn\data\repositories\myrepo"

rem Usually the name of the repository
set dump_name=myrepo

rem Example: 2012_06_25__15_34_35__12
set folder_name_backup=%date:~10,4%_%date:~4,2%_%date:~7,2%__%time:~0,2%_%time:~3,2%_%time:~6,2%__%time:~9,2%
set path_backup=%path_backup%\%folder_name_backup%
set path_backup_hotcopy=%path_backup%\Hotcopy\
set path_backup_working_copy="%path_backup%\Working Copy\"
set path_backup_dump=%path_backup%\Dump\
set steps=4

echo Repository Backup Script for SVN by Matt Refghi
echo mattrefghi.com/blog/subversion-repository-backup-script/
echo.
echo [Step 1 of %steps%] Creating backup folders...
mkdir %path_backup%
mkdir %path_backup_hotcopy%
mkdir %path_backup_working_copy%
mkdir %path_backup_dump%
echo [Step 1 of %steps%] Backup folders created.

echo [Step 2 of %steps%] Starting hotcopy...
svnadmin hotcopy %path_to_repository% %path_backup_hotcopy% --clean-logs
echo [Step 2 of %steps%] Hotcopy complete.

echo [Step 3 of %steps%] Creating dump file...
svnadmin dump %path_to_repository% | "%ProgramFiles%\7-Zip\7z.exe" a %path_backup_dump%\%dump_name%.7z -si%dump_name%.svn
echo [Step 3 of %steps%] Dump file created.

echo [Step 4 of %steps%] Creating copy of working directory...
xcopy.exe /s /e /y /i %path_working_copy% %path_backup_working_copy%
echo [Step 4 of %steps%] Working directory copied.

echo.
echo SVN backup complete.
pause
```