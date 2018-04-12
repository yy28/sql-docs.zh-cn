---
title: 备份和还原数据库使用 SQL Operations Studio (preview) |Microsoft 文档
description: 了解如何备份和还原数据库使用 SQL Operations Studio (preview)
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46ef55aa54275e356eff9674aac10a27b36d758e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>备份和还原使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]

在本教程中，你将学习如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]到：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 查看还原任务的状态

## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server *TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>备份数据库

1. 打开 TutorialDB 数据库仪表板 (打开**服务器**侧栏 (**CTRL + G**)，展开**数据库**，右键单击**TutorialDB**，然后选择**管理**)。 

2. 打开**Backup database**对话框 (单击**备份**上**任务**小组件)。

   ![任务小组件](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教程使用的默认备份选项，因此单击**备份**。
   ![备份的对话框](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

单击后**备份**、 **Backup database**对话框消失，备份过程开始。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>查看备份状态并查看备份脚本

1. 打开**任务历史记录**侧栏上单击的时钟图标*操作栏*或按**CTRL + T**。

   ![任务历史记录](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 若要查看备份脚本在编辑器中，右键单击**成功的备份数据库**和选择**脚本**。

   ![备份脚本](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>从备份文件还原数据库


1. 打开**服务器**侧栏 (**CTRL + G**)，右键单击你的服务器，然后选择**管理**。 

2. 打开**还原数据库**对话框 (单击**还原**上**任务**小组件)。

2. 选择**备份文件**中**从还原**字段。 

3. 单击省略号 （...） 以**备份文件路径**字段，并选择的最新备份文件*TutorialDB*。

3. 类型**TutorialDB_Restored**中**目标数据库**字段**目标**部分，以将备份文件还原到新的数据库。

   ![还原 (restore)](./media/tutorial-backup-restore-sql-server/restore.png)

4. 单击**还原**

5. 若要查看的还原操作的状态，请单击**CTRL + T**以打开**任务历史记录**侧栏。

   ![还原 (restore)](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


在本教程中，您学习了如何：
> [!div class="checklist"]
> * 备份数据库 
> * 查看备份状态
> * 生成用于执行备份的脚本
> * 还原数据库
> * 查看还原任务的状态

