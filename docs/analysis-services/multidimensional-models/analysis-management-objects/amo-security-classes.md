---
title: "AMO 安全类 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, security
- security [AMO]
- AMO, security
ms.assetid: e3d5012a-8121-40de-9244-1fc824228693
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c47924ca1262c6d6e283034ed281edf9e790b21b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="amo-security-classes"></a>AMO 安全类
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]本主题包含以下各节：  
  
-   [角色和 RoleMember 对象](#RolesMembers)  
  
-   [权限对象](#Permissions)  
  
 下图显示了本主题中介绍的类之间的关系。  
  
 ![本主题中介绍的 AMO 中的安全类](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-securityclasses.gif "本主题中介绍的 AMO 中的安全类")  
  
##  <a name="RolesMembers"></a>角色和 RoleMember 对象  
 <xref:Microsoft.AnalysisServices.Role> 对象是通过以下方式创建的：将其添加到数据库的角色集合，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Role> 对象更新到服务器中。 必须更新 <xref:Microsoft.AnalysisServices.Role> 对象，才能使用该对象。  
  
 若要删除<xref:Microsoft.AnalysisServices.Role>对象时，它具有要使用的 Drop 方法删除<xref:Microsoft.AnalysisServices.Role>对象。 在角色集合中使用 Remove 方法只会让您在应用程序中看不到该角色，而不会从服务器中删除该角色。 如果存在任何与 <xref:Microsoft.AnalysisServices.Role> 对象关联的权限，则无法删除该对象。  
  
 <xref:Microsoft.AnalysisServices.RoleMember> 对象是通过以下方式创建的：向角色的成员集合添加一个用户，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Role> 对象更新到服务器中。 只允许服务器管理员或数据库管理员创建角色。 必须先将 <xref:Microsoft.AnalysisServices.Role> 对象更新到服务器中，才允许该服务器的任何成员使用已对其授予用户权限的所有对象。  
  
 若要删除 <xref:Microsoft.AnalysisServices.RoleMember> 对象，则必须使用集合的 Remove 方法从集合中删除该对象，然后使用 Update 方法更新角色。  
  
 有关可用于这些对象的方法和属性的详细信息，请参阅 <xref:Microsoft.AnalysisServices.Role> 中的 <xref:Microsoft.AnalysisServices.RoleMember> 和 <xref:Microsoft.AnalysisServices>。  
  
##  <a name="Permissions"></a>权限对象  
 <xref:Microsoft.AnalysisServices.Permission> 对象是通过以下方式创建的：将其添加到对象的权限集合，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Permission> 对象更新到服务器中。  
  
 若要删除 <xref:Microsoft.AnalysisServices.Permission> 对象，必须使用该对象的 Drop 方法来删除。 在权限集合中使用 Remove 方法只会让您在应用程序中看不到该权限，而不会从服务器中删除 <xref:Microsoft.AnalysisServices.Permission> 对象。 如果存在任何与该角色关联的权限，则无法删除该角色。  
  
 有关可用方法和属性的详细信息，请参阅<xref:Microsoft.AnalysisServices.Permission>中<xref:Microsoft.AnalysisServices>。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [编程 AMO 安全对象](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [权限和访问权限 &#40;Analysis Services-多维数据 &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [逻辑体系结构 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
