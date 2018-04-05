---
Title: 'Tutorial: Additional Tips and Tricks for using SSMS'
description: '介绍使用 SSMS 的一些其他提示和技巧的教程。 '
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
ms.openlocfilehash: 792d6c7fe69a1b8ec77c70d0fbfa6ceaa92d808a
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>教程：使用 SSMS 的其他提示和技巧
本教程将提供一些使用 SQL Server Management Studio 的其他技巧。 本文将指导如何： 

> [!div class="checklist"]
> * 注释/取消注释 Transact-SQL (T-SQL) 文本
> * 缩进文本
> * 在对象资源管理器中筛选对象
> * 访问 SQL Server 错误日志
> * 查找 SQL Server 实例的名称

## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio、针对 SQL Server 的访问权限以及 AdventureWorks 数据库。 

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks 示例数据库](https://github.com/Microsoft/sql-server-samples/releases)。 此处提供在 SSMS 中还原数据库的说明：[还原数据库](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 

## <a name="comment--uncomment-your-t-sql-code"></a>注释/取消注释 T-SQL 代码
可使用工具栏中的注释按钮注释和取消注释部分文本。 系统不会执行已注释掉的文本。 

1. 打开 SQL Server Management Studio。 
2. 连接到 SQL Server。
3. 打开“新建查询”窗口。 
4. 将以下 T-SQL 代码片段粘贴到文本窗口： 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 


5. 突出显示文本的“更改数据库”部分并单击工具栏中的“注释”： 

    ![注释](media/ssms-tricks/comment.png)
6. 单击“执行”运行取消注释的文本部分。 
7. 突出显示除“更改数据库”命令以外的全部内容，然后单击工具栏中的“注释”：

    ![注释全部内容](media/ssms-tricks/commenteverything.png)

8. 突出显示“更改数据库”部分，然后单击“取消注释”对其取消注释：

    ![取消注释](media/ssms-tricks/uncomment.png)
    
9. 单击“执行”运行取消注释的文本部分。 

## <a name="indent-your-text"></a>缩进文本
通过缩进按钮，可以增加和减少文本的缩进。 

1. 打开“新建查询”窗口。 
2. 将以下 T-SQL 代码片段粘贴到文本窗口： 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 
 
3. 突出显示文本的“更改数据库”部分，在工具栏上按“增加缩进”向前移动此文本：

    ![增加缩进](media/ssms-tricks/increaseindent.png)

4. 再次突出显示文本的“更改数据库”部分，此时请单击“减少缩进”向后移动此文本。 
    ![减少缩进](media/ssms-tricks/decreaseindent.png)


## <a name="filter-objects-in-object-explorer"></a>在对象资源管理器中筛选对象
当数据库包含多个对象时，通常很难找到特定对象。 若要简化此过程，可以使用筛选对象这一功能。 本部分介绍如何筛选表，但可将相同步骤应用于“对象资源管理器”中的任何其他节点

1. 连接到 SQL Server。
2. 展开“数据库”节点。
3. 展开“AdventureWorks”数据库节点。 
4. 展开“表”节点。 
   - 你将注意到，你可以看到数据库中的所有表。
5. 右键单击“表”节点 >“筛选器” > “筛选器设置”：

    ![筛选器设置](media/ssms-tricks/filtersettings.png)

6. 在“筛选器设置”窗口中，可以修改筛选器设置。 几个示例：
    - 按名称筛选：![按名称筛选](media/ssms-tricks/filterbyname.png)
    - 按架构筛选：![按架构筛选](media/ssms-tricks/filterbyschema.png)

7. 若要清除筛选器，请右键单击“表” > “删除筛选器”

    ![删除筛选器](media/ssms-tricks/removefilter.png)
    


## <a name="access-your-sql-server-error-log"></a>访问 SQL Server 错误日志
错误日志是一个文件，其中包含 SQL Server 中所发生操作的相关详细信息。 可在 SSMS 中对其进行浏览和查询。 此外，此类文件还在磁盘上呈现为 .log 文件。

### <a name="open-error-log-within-ssms"></a>在 SSMS 中打开错误日志
1. 连接到 SQL Server。
2. 展开 **“管理”** 节点。 
3. 展开“SQL Server 日志”节点。 
4. 右键单击“当前”错误日志 >“查看 SQL Server 日志”：

    ![在 SSMS 中查看错误日志](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>在 SSMS 中查询错误日志
1. 连接到 SQL Server。
2. 打开“新建查询”窗口。
3. 将以下 T-SQL 代码片段粘贴到查询窗口：

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. 将单引号中的文本修改为感兴趣的文本。
5. 执行查询并查看结果：
   
    ![查询错误日志](media/ssms-tricks/queryerrorlog.png)


### <a name="find-error-log-location-if-youre-connected-to-sql"></a>如果连接到 SQL，请查找错误日志位置
1. 连接到 SQL Server。
2. 打开“新建查询”窗口。
3. 将以下 T-SQL 代码片段粘贴到查询窗口并单击“执行”：

 ```sql
    SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
  ``` 

4. 结果将显示文件系统中错误日志的位置： 

    ![通过查询查找错误日志](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-error-log-location-if-you-cannot-connect-to-sql"></a>如果无法连接到 SQL，请查找错误日志位置
1. 打开 SQL Server 配置管理器。 
2. 展开“服务”节点。
3. 右键单击 SQL Server 实例 >“属性”：

    ![配置管理器的服务器属性](media/ssms-tricks/serverproperties.PNG)

4. 选择“启动参数”选项卡。
5. 在“现有参数”区域中，“-e”后面的路径是错误日志的位置： 
    
    ![错误日志](media/ssms-tricks/errorlog.png)
    - 你将注意到，此位置中包含多个 errorlog.*。 以 *.log 结尾的错误日志就是当前日志。 以数字结尾的错误日志是以前的日志，因为每次重启 SQL Server 时都将创建新日志。 
6. 在记事本中打开此文件。 

## <a name="determine-sql-server-name"></a>确定 SQL Server 名称...
在连接到 SQL Server 前后，可通过不同方法确定 SQL Server 的名称。  

### <a name="when-you-dont-know-it"></a>...当你不知道时
1. 按照步骤查找[磁盘上的 SQL Server 错误日志](#finding-your-error-log-if-you-cannot-connect-to-sql)。 
2. 在记事本中打开 errorlog.log。 
3. 在其中进行浏览，直到找到文本“服务器名称是”：
  - 单引号中列出的所有内容都是 SQL Server 的名称以及你将连接到的内容：![错误日志中的服务器名称](media/ssms-tricks/servernameinlog.png)。名称的格式为“HOSTNAME\INSTANCENAME”。 如果看到的只是主机名，然后已安装了默认实例，则实例名称是“MSSQLSERVER”。 连接到默认实例时，只需键入主机名以连接到 SQL Server。  

### <a name="once-youre-connected-to-sql"></a>...连接到 SQL 后 
可在三个位置查找连接到的 SQL Server。 

1. 服务器名称将在“对象资源管理器”中列出：

    ![对象资源管理器中的实例名称](media/ssms-tricks/nameinobjectexplorer.png)
2. 服务器名称将在查询窗口中列出：

    ![查询窗口中的名称](media/ssms-tricks/nameinquerywindow.png)
3. 此外，服务器名称还将在“属性窗口”中列出。
    - 若要对其进行访问，请打开“视图”菜单 >“属性窗口”：

    ![属性中的名称](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>...如果连接到别名或可用性组侦听程序 
连接到别名或可用性组侦听程序时，则将显示“对象资源管理器”和“属性”。 在这种情况下，SQL Server 名称可能不是显而易见的，并且必须进行查询。 

1. 连接到 SQL Server。
2. 打开“新建查询”窗口。
3. 将以下 T-SQL 代码片段粘贴到窗口： 

  ```sql
   select @@Servername 
 ``` 
4. 查看查询结果，确定连接到的 SQL Server 的名称： 
    
    ![查询服务器名称](media/ssms-tricks/queryservername.png)


