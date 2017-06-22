---
title: "新用户角色 (Management Studio) |Microsoft 文档"
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
- sql13.swb.reportserver.newrole.f1
ms.assetid: 9f76a235-0b58-479c-8e5b-50588091b71c
caps.latest.revision: 26
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d4c239e87379ead3b826e4db3c85006b364392a6
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="new-user-role-management-studio"></a>新建用户角色 (Management Studio)
  使用此页可以创建项级角色定义。 项级角色定义是一组任务的命名集合，这些任务用于枚举用户对于文件夹、报表、模型、资源和共享数据源可以执行的任务。 例如，预定义“浏览者”角色就是属于项级角色定义。该角色可以标识报表最终用户在浏览文件夹和查看报表时可能需要执行的各种操作。  
  
 角色定义的数量不应该很多。 大多数单位都只要求几个角色定义。 但是，如果预定义的角色定义不能满足需要，您可以对其进行修改或创建新的角色定义。  
  
> [!NOTE]  
>  角色分配仅适用于在本机模式下运行的报表服务器。 如果针对报表服务器配置了 SharePoint 集成，则此页不可用。  
  
## <a name="options"></a>选项  
 **名称**  
 键入角色定义的名称。 角色定义名称在报表服务器命名空间中必须是唯一的。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时请不要使用以下字符：  
  
 ; ? : @ & = + , $ / * < >  
  
 " /  
  
 **Description**  
 键入介绍如何使用角色和枚举角色所支持任务的说明。  
  
 **任务**  
 选择可通过此角色执行的任务。 不能创建新任务或修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支持的现有任务。 在项级角色定义中只能使用项级任务。  
  
 **任务说明**  
 显示任务说明，其中枚举了任务所支持的操作或权限。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [角色定义](../../reporting-services/security/role-definitions.md)  
  
  

