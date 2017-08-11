---
title: "新建系统角色 (Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.newsystemrole.f1
ms.assetid: 7b4a0b98-975b-478a-8359-7db39ccbb347
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f4917fea7fbaa0f652287a08e0a3a5727feaad9e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="new-system-role-management-studio"></a>新建系统角色 (Management Studio)
  使用此页可以创建系统级角色定义。 系统角色定义指定了作为整体应用于报表服务器的一组系统级任务。  
  
> [!NOTE]  
>  角色分配仅适用于在本机模式下运行的报表服务器。 如果针对报表服务器配置了 SharePoint 集成，则此页不可用。  
  
## <a name="options"></a>选项  
 **名称**  
 键入角色定义的名称。 角色定义名称在报表服务器命名空间中必须是唯一的。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时请不要使用以下字符：  
  
 ; ? : @ & = + , $ / * < >  
  
 " /  
  
 **Description**  
 提供介绍如何使用角色和枚举角色所支持任务的说明。  
  
 **任务**  
 选择可通过此角色执行的系统级任务。 不能创建新任务或修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支持的现有任务。 不能为系统角色定义选择项级任务。  
  
 **任务说明**  
 显示任务说明，其中枚举了任务所支持的操作或权限。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio F1 帮助中的报表服务器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [角色定义](../../reporting-services/security/role-definitions.md)  
  
  

