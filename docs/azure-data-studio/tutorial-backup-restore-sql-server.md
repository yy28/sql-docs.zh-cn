---
title: 备份和还原数据库
titleSuffix: Azure Data Studio
description: 了解如何备份和还原使用 Azure Data Studio 的数据库
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 5550a1151ed0fb71a769e7990d9cd47b3e9b0e47
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089695"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>备份和还原数据库使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

您可以在本教學課程中，了解如何使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 來完成下列工作：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 檢視還原工作的狀態

## <a name="prerequisites"></a>必备条件

本教程需要 SQL Server *TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [使用 SQL Server 连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

本教程需要连接到 SQL Server 数据库。 Azure SQL 数据库还具有自动化备份，因此，Azure Data Studio 不会执行 Azure SQL 数据库备份和还原。 有关详细信息，请参阅[了解有关 SQL 数据库自动备份信息](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)。

## <a name="backup-a-database"></a>备份数据库

1. 打开 TutorialDB 数据库仪表板 (打开**服务器**侧栏 (**CTRL + G**)，展开**数据库**，右键单击**TutorialDB**，然后选择**管理**)。

2. 開啟 **Backup database** 對話方塊 (按一下**工作**小工具上的**備份**)。

   ![任务小组件](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教程使用的默认备份选项，因此，请单击**备份**。
   ![备份对话框](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

单击后**备份**，则**备份数据库**对话框消失，备份过程开始。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>查看备份状态并查看备份脚本

1. 在**動作列**上按一下 [時鐘] 圖示或按下 *CTRL + T*，以開啟**工作歷程記錄**資訊看板。

   ![任务历史记录](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 若要在編輯器內檢視備份指令碼，請以滑鼠右鍵按一下**成功的備份資料庫**並選取**指令碼**。

   ![备份脚本](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>從備份檔案還原資料庫


1. 開啟**伺服器**資訊看板 (**CTRL + G**)，以滑鼠右鍵按一下您的伺服器，然後選取**管理**。 

2. 開啟**還原資料庫**對話方塊 (按一下**工作**小工具上的**還原**)。

2. 选择**备份文件**中**从还原**字段。 

3. **從還原**欄位中選取*備份檔案*。 

3. 在**目的地**區段的**目標資料庫**欄位中輸入 **TutorialDB_Restored**，以將備份檔案還原至新的資料庫。

   ![还原 (restore)](./media/tutorial-backup-restore-sql-server/restore.png)

4. 单击**还原**

5. 若要查看的还原操作的状态，请按**CTRL + T**以打开**任务历史记录**侧栏。

   ![还原 (restore)](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


在本教程中，你将了解：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 檢視還原工作的狀態

