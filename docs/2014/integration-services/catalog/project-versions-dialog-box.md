---
title: “项目版本”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8aefce0d5afe7bec37c5fe49ba63c3fec61f3747
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771535"
---
# <a name="project-versions-dialog-box"></a>“项目版本”对话框
  使用 **“项目版本”** 对话框可以查看项目版本和还原以前的版本。  
  
 你还可以在 [catalog.object_versions（SSISDB 数据库）](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database)视图中查看先前版本，以及使用[catalog.restore_project（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database)存储过程还原先前版本。  
  
 **您希望做什么？**  
  
-   [打开“项目版本”对话框](#open_dialog)  
  
-   [还原项目版本](#restore)  
  
##  <a name="open_dialog"></a> 打开“项目版本”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 服务器。  
  
     也就是说，连接到承载 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“Integration Services 目录”** 节点以显示 **SSISDB** 节点。  
  
4.  **SSISDB** 节点包含一个或多个文件夹，每个文件夹包含一个或多个项目。 展开包含您感兴趣的项目的文件夹。  
  
5.  右键单击该项目，然后单击“版本”。   
  
 在“项目版本”对话框中，“版本”表显示服务器上已部署的项目的版本列表，并显示部署版本的日期和时间、还原版本的日期和时间（如果被还原过）、版本说明以及版本标识符。   当前活动版本用表的 **“当前”** 列中的复选标记表示。  
  
##  <a name="restore"></a> 还原项目版本  
 若要还原项目的以前版本，请在 **“版本”** 表中选择该版本，然后单击 **“还原到所选版本”** 。 项目将还原到所选版本，且该版本用 **“版本”** 表的 **“当前”** 列中的复选标记表示。  
  
  
