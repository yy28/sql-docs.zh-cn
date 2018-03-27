---
Title: 'Tutorial: Script Objects in SQL Server Management Studio'
description: 有关在 SSMS 中编写对象脚本的教程。
keywords: SQL Server, SSMS, SQL Server Management Studio, 脚本, 编写脚本
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: 2ee56bc26c22f91af7bf156ea967c19b61eab881
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>教程：在 SQL Server Management Studio 中编写对象脚本
本教程将指导如何为 SQL Server Management Studio 中找到的各种对象生成 Transact-SQL (T-SQL) 脚本。  本教程提供如何编写以下对象的脚本的示例： 
 - 在 GUI 中执行操作时的查询
 - 两种不同方式（“脚本编写为”和“生成脚本”）的数据库
 - 表
 - 存储过程
 - 扩展事件

本教程摘要：可为“对象资源管理器”中的任何对象编写脚本，方法是右键单击该对象并选择“编写对象脚本为”选项。 


## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio、针对 SQL Server 的访问权限以及 AdventureWorks 数据库。 

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- 下载 [AdventureWorks 示例数据库](https://github.com/Microsoft/sql-server-samples/releases)。 
    - 此处提供在 SSMS 中还原数据库的说明：[还原数据库](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 


## <a name="script-queries-from-gui"></a>从 GUI 编写查询脚本
在使用 SSMS 中的 GUI 执行任务时，还可以生成与该任务相关联的 T-SQL 代码。 以下示例演示如何在备份数据库和收缩事务日志时执行此操作。  可以向通过 GUI 完成的任何操作应用这些相同的步骤。 

### <a name="scriptt-sql-when-backing-up-a-database"></a>备份数据库时编写 T-SQL 脚本
1. 连接到 SQL Server。
2. 展开 **“数据库”** 节点。
3. 右键单击数据库>“任务” > “备份”：

    ![备份数据库](media/scripting-ssms/backupdb.png)

4. 按照所需方式配置备份。 对于本教程，所有内容均保留默认值。 但是，在窗口中进行的任何更改都会反映在脚本中。 
5. 单击选项“脚本” > “将操作脚本写入查询窗口”：
 
    ![编写 DB 备份脚本](media/scripting-ssms/scriptdbbackup.PNG)
6. 查看查询窗口中填充的 T-SQL： 

    ![DB 备份的脚本](media/scripting-ssms/dbbackupscript.PNG)


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>在收缩事务日志时编写 T-SQL 脚本
1. 右键单击数据库>“任务” > “收缩” > “文件”：

     ![收缩文件](media/scripting-ssms/shrinkfiles.png)

2. 从“文件类型”下拉列表中选择“日志”：

    ![收缩事务日志](media/scripting-ssms/shrinktlog.png)

3. 单击选项“脚本”和“将操作脚本保存到剪贴板”：

    ![将脚本保存到剪贴板](media/scripting-ssms/scriptactiontoclipboard.png)

4. 打开“新建查询”窗口并粘贴（在窗口中右键单击 >“粘贴”）：

    ![粘贴脚本](media/scripting-ssms/paste.png)


## <a name="script-databases"></a>编写数据库脚本
以下部分介绍如何使用“脚本编写为”选项和“生成脚本”选项编写数据库脚本。  “脚本编写为”选项将重新创建数据库及其配置选项。 “生成脚本”选项将编写数据库中所有对象（数据除外）的脚本。 若还要编写数据脚本，则需使用[导入和导出向导](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/start-the-sql-server-import-and-export-wizard)。  


### <a name="script-database-using-script-option"></a>使用“脚本”选项编写数据库脚本
1. 连接到 SQL Server。
2. 展开 **“数据库”** 节点。
3. 右键单击数据库 >“编写数据库脚本为”：

    ![编写 DB 脚本](media/scripting-ssms/scriptdb.png)

4. 在窗口中查看数据库创建查询： 

    ![已编写脚本的 DB](media/scripting-ssms/scriptedoutdb.png)
    - 此选项将仅编写数据库配置选项的脚本。  

### <a name="script-database-using-generate-scripts-option"></a>使用“生成脚本”选项编写数据库脚本
1. 连接到 SQL Server。
2. 展开 **“数据库”** 节点。
3. 右键单击数据库 >“任务” > “生成脚本”：

    ![生成 DB 的脚本](media/scripting-ssms/generatescriptsfordb.png)

4. 选择“下一步”，然后可以选择编写整个数据库的脚本或编写数据库中特定对象的脚本： 
 
    ![生成对象的脚本](media/scripting-ssms/scriptobjects.png)
 
5. 选择“下一步” 。 可在此屏幕中配置脚本的保存位置。 
    - 此外，还可以通过选择“高级”配置高级选项：

    ![高级脚本选项](media/scripting-ssms/advancedscripts.png)

6. 准备好继续操作后，一直点击“下一步”直至生成脚本，然后转到“完成”。 数据库脚本将位于步骤 5 中保存的位置。 
    - 这将编写数据库中架构和各种对象（数据除外）的脚本。 
 
## <a name="script-tables"></a>编写表脚本
本部分介绍如何编写数据库中表的脚本。

1. 连接到 SQL Server。
2. 展开“数据库”节点。
3. 展开“AdventureWorks”数据库节点。 
4. 展开“表”节点。
5. 右键单击要编写脚本的表 >“编写表脚本为”
    - 此处提供各种选项，例如创建表或向表中插入数据： 
    
    ![编写表脚本](media/scripting-ssms/scripttable.png)
 
## <a name="script-stored-procedures"></a>编写存储过程脚本
本部分介绍如何编写存储过程脚本。 

1. 连接到 SQL Server。
2. 展开“数据库”节点。
3. 展开“可编程性”节点。 
4. 展开“存储过程”节点。
5. 右键单击感兴趣的存储过程 >“编写存储过程脚本为”
    
    ![编写存储过程脚本](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>编写扩展事件脚本
本部分介绍如何编写[扩展事件](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events)脚本。 

1. 连接到 SQL Server。
2. 展开“管理”节点。
3. 展开“扩展事件”节点。
4. 展开“会话”节点。
5. 右键单击感兴趣的扩展会话 >“编写会话脚本为”：

    ![编写 xEvent 脚本](media/scripting-ssms/scriptxevents.png) 

## <a name="next-steps"></a>后续步骤
下一篇文章将介绍 SSMS 中提供的预建模板。 

转到下一篇文章，了解详细信息
> [!div class="nextstepaction"]
> [后续步骤按钮](templates-ssms.md)


