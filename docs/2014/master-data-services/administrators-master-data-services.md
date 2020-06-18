---
title: 管理员 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: aeedc1f735fd296169f704b794d1bb0e69adab22
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972267"
---
# <a name="administrators-master-data-services"></a>管理员 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中有两种类型的管理员：模型管理员和 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系统管理员。  
  
## <a name="model-administrators"></a>模型管理员  
 在中 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ，模型管理员是对 "**模型对象**" 选项卡上的顶级模型对象具有 "**更新**" 权限且未分配其他任何权限的用户。  
  
-   如果用户具有对 **“资源管理器”** 功能区域的访问权限，此用户可以添加、删除和更新此区域中的所有主数据。  
  
-   如果用户具有对其他功能区域的访问权限，则此用户可以执行该功能区域中的所有管理任务。  
  
 每个模型可以有多个管理员。 每个用户可以是 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 部署中一个、多个或所有模型的模型管理员。  
  
 可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中或通过编程方式将用户配置为模型管理员。 有关详细信息，请参阅 [创建模型管理员 (Master Data Services)](create-a-model-administrator-master-data-services.md)。  
  
## <a name="master-data-services-system-administrator"></a>Master Data Services 系统管理员  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系统管理员只有一个。 系统管理员是在创建数据库时为**管理员帐户**指定的用户 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系统管理员：  
  
-   自动对所有功能区域具有访问权限。  
  
-   可以添加、删除和更新 "**资源管理器**" 功能区域中所有模型的所有主数据。  
  
 您可以更改指派为系统管理员的用户。 有关详细信息，请参阅[&#40;Master Data Services&#41;更改系统管理员帐户](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
## <a name="comparing-administrator-types"></a>比较管理员类型  
  
|管理员类型|说明|  
|------------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系统管理员|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中分配的权限对于管理员的访问权限没有影响。<br /><br /> 自动对所有模型具有 "**更新**" 权限。<br /><br /> 自动对所有功能区域具有访问权限。<br /><br /> 在 tblUser 中， **ID**列中的值为**1**。|  
|模型管理员|在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中分配的权限确定用户是否为模型管理员。<br /><br /> 基于显式分配的权限或者从组继承的权限，用户可以是模型管理员。<br /><br /> 仅适用于具有分配给顶级模型对象的 "**更新**" 权限且没有其他权限的模型的管理员。<br /><br /> 仅对向其分配访问权限的功能区域具有访问权限。<br /><br /> 在 tblUser 中， **ID**列中的值不是**1**。|  
  
## <a name="see-also"></a>另请参阅  
 [创建模型管理员 &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [更改系统管理员帐户 &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [创建 Master Data Services 数据库](install-windows/create-a-master-data-services-database.md)   
 [通知 (Master Data Services)](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
