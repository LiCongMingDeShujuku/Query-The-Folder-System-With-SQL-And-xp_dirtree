![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 使用xp_dirtree查询文件夹系统
#### Query The Folder System With xp_dirtree
**发布-日期: 2014年12月15日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
下面是一小段SQL逻辑，它将为你提供文件夹列表或来自任何的文件。你所需要的只是从SQL服务帐户或常规使用帐户MyDomain \ MyUserName访问这些文件夹的权限。


## English
Here’s a short piece of SQL Logic that will give you a list of folders, or files from any directory. All you need is access rights to those folders either from the SQL Service account or your regular use account MyDomain\MyUserName.

---
## Logic
```SQL
use master;
set nocount on
 
if object_id('tempdb..#folderandfileinfo') is not null
drop table #folderandfileinfo
 
create table #folderandfileinfo
(
cid int identity(1,1) primary key clustered
,   subdirectory    varchar(255)
,   depth int
,   isfile int
)
 
declare @path   varchar(255)
set @path   = '\\MyBackupShare\MyFolderName' -- insert your path here.
 
insert into #folderandfileinfo
(
[subdirectory]
,   [depth]
,   [isfile]
)
exec master..xp_dirtree
@path
,   1
,   1
 
select
subdirectory
,   depth
,   'object' = case isFile when '1' then 'File' when '0' then 'Folder' end from
#folderandfileinfo
where
subdirectory like '%.bak'


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

