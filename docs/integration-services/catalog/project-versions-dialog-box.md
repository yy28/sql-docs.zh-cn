---
title: “项目版本”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84554c1ac7da7fedfdde85b0127c0c3e84c4eccc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="project-versions-dialog-box"></a>“项目版本”对话框
  使用 **“项目版本”** 对话框可以查看项目版本和还原以前的版本。  
  
 你还可以在 [catalog.object_versions（SSISDB 数据库）](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)视图中查看先前版本，以及使用[catalog.restore_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)存储过程还原先前版本。  
  
 **您希望做什么？**  
  
-   [打开“项目版本”对话框](#open_dialog)  
  
-   [还原项目版本](#restore)  
  
##  <a name="open_dialog"></a> 打开“项目版本”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
     也就是说，连接到承载 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“Integration Services 目录”** 节点以显示 **SSISDB** 节点。  
  
4.  **SSISDB** 节点包含一个或多个文件夹，每个文件夹包含一个或多个项目。 展开包含您感兴趣的项目的文件夹。  
  
5.  右键单击该项目，然后单击“版本”。  
  
 在“项目版本”对话框中，“版本”表显示服务器上已部署的项目的版本列表，并显示部署版本的日期和时间、还原版本的日期和时间（如果被还原过）、版本说明以及版本标识符。 当前活动版本用表的 **“当前”** 列中的复选标记表示。  
  
##  <a name="restore"></a> 还原项目版本  
 若要还原项目的以前版本，请在 **“版本”** 表中选择该版本，然后单击 **“还原到所选版本”**。 项目将还原到所选版本，且该版本用 **“版本”** 表的 **“当前”** 列中的复选标记表示。  
  
  
