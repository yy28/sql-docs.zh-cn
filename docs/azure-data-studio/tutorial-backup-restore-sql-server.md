---
title: 备份和还原数据库
description: 请按照本教程的说明操作，了解如何使用 Azure Data Studio 备份和还原数据库。
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 5e276a830f5fa6abc9b1fcf70c540d4cb955d5af
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522421"
---
# <a name="backup-and-restore-databases-using-azure-data-studio"></a>使用 Azure Data Studio 备份和还原数据库

在本教程中，将了解如何使用 Azure Data Studio 执行以下操作：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 查看还原任务的状态

## <a name="prerequisites"></a>先决条件

本教程需要 SQL Server TutorialDB。 若要创建 TutorialDB 数据库，请完成以下其中一项快速入门：

* [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 连接并查询 SQL Server](quickstart-sql-server.md)

本教程需要连接到 SQL Server 数据库。 Azure SQL 数据库已自动备份，因此 Azure Data Studio 不执行 Azure SQL 数据库备份和还原。 有关详细信息，请参阅[了解 SQL 数据库自动备份](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)。

## <a name="back-up-a-database"></a>备份数据库

1. 打开 TutorialDB 数据库仪表板（打开“服务器”边栏 (Ctrl+G)，展开“数据库”，右键单击“TutorialDB”，然后选择“管理”）    。

2. 打开“备份数据库”对话框（在“任务”小组件上单击“备份”）  。

   ![任务小组件](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教程使用默认备份选项，因此请单击“备份”。
   ![备份对话框](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

单击“备份”后，“备份数据库”对话框将会消失，备份过程将开始 。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>查看备份状态和查看备份脚本

1. “任务历史记录”窗格将出现，否则请按 CTRL+T 。

   ![任务历史记录](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 要在编辑器中查看备份脚本，请右键单击“已成功备份的数据库”，然后选择“脚本” 。

   ![备份脚本](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>从备份文件中还原数据库

1. 打开“服务器”边栏 (Ctrl+G)，右键单击服务器，然后选择“管理”  。

2. 打开“还原数据库”对话框（在“任务”小组件上单击“还原”）  。

   ![还原任务](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. 在“还原来源”字段中选择“备份文件” 。

4. 单击“备份文件路径”字段中的省略号 (...)，然后选择 TutorialDB 的最新备份文件。

5. 在“目标”部分的“目标数据库”字段中，键入“TutorialDB_Restored”以将备份文件还原到新数据库  。 然后选择“还原”。

   ![还原](./media/tutorial-backup-restore-sql-server/restore.png)

6. 要查看还原操作的状态，请按 Ctrl+T，打开“任务历史记录” 。

   ![还原](./media/tutorial-backup-restore-sql-server/task-history-restore.png)