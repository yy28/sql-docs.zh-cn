---
title: 备份和还原数据库使用 SQL 操作 Studio （预览版） |Microsoft 文档
description: 了解如何使用 SQL Operations Studio (預覽) 以備份和還原資料庫
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22a453caa9d29432381da6861a0f0c4e3e61d77e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34582449"
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>备份和还原使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

您可以在本教學課程中，了解如何使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 來完成下列工作：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 檢視還原工作的狀態

## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server *TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>备份数据库

1. 打开 TutorialDB 数据库仪表板 (打开**服务器**侧栏 (**CTRL + G**)，展开**数据库**，右键单击**TutorialDB**，然后选择**管理**)。 

2. 開啟 **Backup database** 對話方塊 (按一下**工作**小工具上的**備份**)。

   ![任务小组件](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教程使用的默认备份选项，因此单击**备份**。
   ![备份的对话框](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

单击后**备份**、 **Backup database**对话框消失，备份过程开始。

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

5. 若要查看还原操作的状态，请按**CTRL + T**以打开**任务历史记录**侧栏。

   ![还原 (restore)](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


在本教程中，您学习了如何：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 檢視還原工作的狀態

