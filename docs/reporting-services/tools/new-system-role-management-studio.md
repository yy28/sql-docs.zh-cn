---
title: 新建系统角色 (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.newsystemrole.f1
ms.assetid: 7b4a0b98-975b-478a-8359-7db39ccbb347
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9b9689be21565aa603433f20b1b445cb5f806c94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823215"
---
# <a name="new-system-role-management-studio"></a>新建系统角色 (Management Studio)
  使用此页可以创建系统级角色定义。 系统角色定义指定了作为整体应用于报表服务器的一组系统级任务。  
  
> [!NOTE]  
>  角色分配仅适用于在本机模式下运行的报表服务器。 如果针对报表服务器配置了 SharePoint 集成，则此页不可用。  
  
## <a name="options"></a>选项  
 **名称**  
 键入角色定义的名称。 角色定义名称在报表服务器命名空间中必须是唯一的。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时请不要使用以下字符：  
  
 ; ? : \@ & = + , $ / * < >  
  
 " /  
  
 **Description**  
 提供介绍如何使用角色和枚举角色所支持任务的说明。  
  
 **任务**  
 选择可通过此角色执行的系统级任务。 不能创建新任务或修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支持的现有任务。 不能为系统角色定义选择项级任务。  
  
 **任务说明**  
 显示任务说明，其中枚举了任务所支持的操作或权限。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [角色定义](../../reporting-services/security/role-definitions.md)  
  
  
