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
ms.openlocfilehash: a931ddb3cf3229970de4b301e18002484acbaf53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>教程：在 SQL Server Management Studio 中编写对象脚本
本教程将指导如何为 SQL Server Management Studio 中找到的各种对象生成 Transact-SQL (T-SQL) 脚本。  本教程提供如何编写以下对象的脚本的示例： 

> [!div class="checklist"]
> * 在 GUI 中执行操作时的查询
> * 两种不同方式（“脚本编写为”和“生成脚本”）的数据库
> * 表
> * 存储过程
> * 扩展事件

本教程摘要：可为“对象资源管理器”中的任何对象编写脚本，方法是右键单击该对象并选择“编写对象脚本为”选项。 


## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio、针对 SQL Server 的访问权限以及 AdventureWorks 数据库。 

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks2016 示例数据库](https://github.com/Microsoft/sql-server-samples/releases)。 此处提供在 SSMS 中还原数据库的说明：[还原数据库](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 


## <a name="script-queries-from-gui"></a>从 GUI 编写查询脚本
在使用 SSMS 中的 GUI 执行任务时，还可以生成与该任务相关联的 T-SQL 代码。 以下示例演示如何在备份数据库和收缩事务日志时执行此操作。  可以向通过 GUI 完成的任何操作应用这些相同的步骤。 

### <a name="script-t-sql-when-backing-up-a-database"></a>备份数据库时编写 T-SQL 脚本
1. 连接到 SQL Server。
2. 展开 **“数据库”** 节点。
3. 右键单击“AdventureWorks2016”数据库 >“任务” > “备份”：

    ![备份数据库](media/scripting-ssms/backupdb.png)

4. 按照所需方式配置备份。 对于本教程，所有内容均保留默认值。 但是，在窗口中进行的任何更改都会反映在脚本中。 
5. 选择选项“脚本” > “将操作脚本写入查询窗口”：
 
    ![编写 DB 备份脚本](media/scripting-ssms/scriptdbbackup.PNG)
6. 查看查询窗口中填充的 T-SQL： 

    ![DB 备份的脚本](media/scripting-ssms/dbbackupscript.PNG)
7. 选择“执行”以执行查询，以便通过 T-SQL 备份数据库。 


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>在收缩事务日志时编写 T-SQL 脚本
1. 右键单击“AdventureWorks2016”数据库 >“任务” > “收缩” > “文件”：

     ![收缩文件](media/scripting-ssms/shrinkfiles.png)

2. 从“文件类型”下拉列表中选择“日志”：

    ![收缩事务日志](media/scripting-ssms/shrinktlog.png)

3. 选择选项“脚本”和“将操作脚本保存到剪贴板”：

    ![将脚本保存到剪贴板](media/scripting-ssms/scriptactiontoclipboard.png)

4. 打开“新建查询”窗口并粘贴（在窗口中右键单击 >“粘贴”）：

    ![粘贴脚本](media/scripting-ssms/paste.png)
5. 选择“执行”以执行查询和收缩事务日志。 


## <a name="script-databases"></a>编写数据库脚本
以下部分介绍如何使用“脚本编写为”选项和“生成脚本”选项编写数据库脚本。  “脚本编写为”选项将重新创建数据库及其配置选项。 通过“生成脚本”选项，可编写架构和数据的脚本。 在本部分中，将创建两个新的数据库，使用“脚本编写为”选项创建 AdventureWorks2016a。 将使用“生成脚本”选项创建 AdventureWorks2016b。 


### <a name="script-database-using-script-option"></a>使用“脚本”选项编写数据库脚本
1. 连接到 SQL Server。
2. 展开 **“数据库”** 节点。
3. 右键单击“AdventureWorks2016”数据库 >“编写数据库脚本为” > “创建到” > “新建查询窗口”：

    ![编写 DB 脚本](media/scripting-ssms/scriptdb.png)

4. 在窗口中查看数据库创建查询： 

    ![已编写脚本的 DB](media/scripting-ssms/scriptedoutdb.png)
    - 此选项将仅编写数据库配置选项的脚本。
5. 选择键盘上的 Ctrl+F 打开“查找”对话框并选择向下箭头以打开“替换”选项。 在顶部的“查找”行中键入“AdventureWorks2016”，在底部的“替换”行中键入“AdventureWorks2016a”。 
6. 选择“全部替换”，将所有 AdventureWorks2016 实例替换为 AdventureWorks2016a。 

    ![查找和替换](media/scripting-ssms/findandreplace.png)

1. 选择“执行”以执行查询并创建新的 AdventureWorks2016a 数据库。 

### <a name="script-database-using-generate-scripts-option"></a>使用“生成脚本”选项编写数据库脚本
1. 连接到 SQL Server。
2. 展开 **“数据库”** 节点。
3. 右键单击“AdventureWorks2016”数据库 >“任务” > “生成脚本”：

    ![生成 DB 的脚本](media/scripting-ssms/generatescriptsfordb.png)

4. 随即会打开“简介”页，选择“下一步”打开“选择对象”页。 可选择整个数据库或数据库中的特定对象。 选择对应选项，编写整个数据库及所有数据库对象的脚本 
 
    ![生成对象的脚本](media/scripting-ssms/scriptobjects.png)
 
5. 选择“下一步”打开“设置脚本编写选项”页，可在其中配置保存脚本的位置以及其他高级选项。 

    A. 选择对应选项，保存到新查询窗口。 

    B. 选择“高级”并确保已设置以下选项： 

      - “编写统计信息脚本”设置为“编写统计信息脚本”
      - “要编写脚本的数据的类型”设置为“仅限架构”
      - “编写索引脚本”设置为“true”

   ![脚本对象](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > 如果为“要编写脚本的数据的类型”选择“架构和数据”，可以为数据库的数据编写脚本。 但是，这不适用于大型数据库，因为它需要的内存多于 SSMS 能够分配的。 这对小型数据库是可行的，但如果要移动大型数据库的数据，应该使用[导入和导出向导](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)。



1. 选择“确定”，然后选择“下一步”。 
2. 选择“摘要”上的“下一步”，然后再次选择“下一步”，以将脚本生成到“新建查询”窗口。  
3. 选择键盘上的 Ctrl+F 打开“查找”对话框并选择向下箭头以打开“替换”选项。 在顶部的“查找”行中键入“AdventureWorks2016”，在下面的“替换”行中键入“AdventureWorks2016b”。 
    A. 选择“全部替换”以将所有 AdventureWorks2016 实例替换为 AdventureWorks2016b。 

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)
7. 选择“执行”以执行查询并创建新的 AdventureWorks2016b 数据库。 
 
## <a name="script-tables"></a>编写表脚本
本部分介绍如何编写数据库中表的脚本。 使用此选项，可以创建表，或删除并创建表。 通过此选项，还可以编写与修改表（例如，插入或更新表）有关的 T-SQL 的脚本。 在此部分中，将删除表，并重新创建它。 

1. 连接到 SQL Server。
2. 展开“数据库”节点。
3. 展开“AdventureWorks”数据库节点。 
4. 展开“表”节点。
5. 右键单击“dbo.ErrorLog” >  “编写表脚本为” > “删除并创建到” > “新查询编辑器窗口”：
    
    ![编写表脚本](media/scripting-ssms/scripttable.png)

6. 选择执行，以执行查询，这会删除 Errorlog 表并重新创建它。 

    >[!NOTE]
    > 默认情况下，AdventureWorks2016 数据库中的 Errorlog 表为空，因此删除该表不会丢失任何数据。 但是，在具有数据的表上执行这些步骤会造成数据丢失。 
 
## <a name="script-stored-procedures"></a>编写存储过程脚本
此部分介绍如何删除并创建存储过程。  

1. 连接到 SQL Server。
2. 展开“数据库”节点。
3. 展开“可编程性”节点。 
4. 展开“存储过程”节点。
5. 右键单击存储过程“dbo.uspGetBillOfMaterials”> “编写存储过程脚本为” > “删除并创建到” > “新建查询窗口”：
    
    ![编写存储过程脚本](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>编写扩展事件脚本
本部分介绍如何编写[扩展事件](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events)脚本。 

1. 连接到 SQL Server。
2. 展开“管理”节点。
3. 展开“扩展事件”节点。
4. 展开“会话”节点。
5. 右键单击感兴趣的扩展会话 >“编写会话脚本为” > “新查询编辑器窗口”：

    ![编写 xEvent 脚本](media/scripting-ssms/scriptxevents.png) 
6. 在“新建查询窗口”中，将新的会话名称从 system_health 修改为 system_health2，并选择“执行”，以执行该查询。 

    A. 右键单击“对象资源管理器”中的“会话”并选择“刷新”，以查看新的扩展事件会话。 会话旁边的绿色图标指示会话正在运行中，而红色图标指示会话已停止。 

    ![新建 XEvent](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > 可通过右键单击会话并选择“开始”来开始会话。 但是，由于这是已经在运行的 system_health 会话的副本，可跳过此步骤。 右键单击扩展事件会话副本并选择“删除”，可删除该副本。 

## <a name="next-steps"></a>后续步骤
下一篇文章将介绍 SSMS 中提供的预建 T-SQL 模板。 

转到下一篇文章，了解详细信息：
> [!div class="nextstepaction"]
> [后续步骤](templates-ssms.md)


