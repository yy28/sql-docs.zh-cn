---
title: 属性组 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a7f0849e5549c904c63225b817a0548c13155247
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687938"
---
# <a name="attribute-groups-master-data-services"></a>属性组 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，属性组帮助组织实体中的属性。 如果实体具有很多属性，属性组可以改进实体在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中显示的方式。  
  
## <a name="how-attribute-groups-change-the-display"></a>属性组如何更改显示方式  
 属性组显示为 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的“资源管理器”功能区域的网格上的选项卡。  
  
 在某一实体具有大量属性并且您在 **“资源管理器”** 的网格中查看该实体时，必须向右滚动以便查看所有属性。 若要禁止这一滚动，您可以创建属性组。  
  
-   属性组始终包括 Name 和 Code 属性。  
  
-   一个实体的每个属性都可以属于一个或多个属性组。  
  
-   所有属性将自动包含在 **“资源管理器”** 的 **“所有属性”** 选项卡上。  
  
-   没有办法隐藏 **“所有属性”** 选项卡。  
  
 属性组在 **的** “系统管理” [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]功能区域中进行管理。  
  
## <a name="show-or-hide-attribute-groups"></a>显示或隐藏属性组  
 创建属性组时，对除创建者之外的所有用户自动隐藏它。 有关使组可见的详细信息，请参阅 [使属性组对用户可见 (Master Data Services)](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)选项卡上。  
  
 如果要隐藏组中的特定属性，可以将 **“拒绝”** 权限分配给该属性。 有关详细信息，请参阅[叶权限 &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|创建新的属性组并向其中添加属性。|[创建属性组 (Master Data Services)](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|使属性组对用户可见。|[使属性组对用户可见 (Master Data Services)](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|更改现有属性组的名称。|[更改属性组名称 (Master Data Services)](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|删除现有属性组。|[删除属性组 (Master Data Services)](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [属性 (Master Data Services)](../master-data-services/attributes-master-data-services.md)  
  
  
