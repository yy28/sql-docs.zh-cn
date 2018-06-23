---
title: AMO 安全类 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Analysis Management Objects, security
- security [AMO]
- AMO, security
ms.assetid: e3d5012a-8121-40de-9244-1fc824228693
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9562c7aab750f4114ef59c1a7c17f44c8e3b05e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138958"
---
# <a name="amo-security-classes"></a>AMO 安全类
  
 下图显示了本主题中介绍的类之间的关系。  
  
 ![本主题中介绍的 AMO 中的安全类](../../../analysis-services/dev-guide/media/amo-securityclasses.gif "本主题中介绍的 AMO 中的安全类")  
  
##  <a name="RolesMembers"></a> 角色和 RoleMember 对象  
 <xref:Microsoft.AnalysisServices.Role> 对象是通过以下方式创建的：将其添加到数据库的角色集合，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Role> 对象更新到服务器中。 必须更新 <xref:Microsoft.AnalysisServices.Role> 对象，才能使用该对象。  
  
 若要删除<xref:Microsoft.AnalysisServices.Role>对象时，它具有要使用的 Drop 方法删除<xref:Microsoft.AnalysisServices.Role>对象。 在角色集合中使用 Remove 方法只会让您在应用程序中看不到该角色，而不会从服务器中删除该角色。 如果存在任何与 <xref:Microsoft.AnalysisServices.Role> 对象关联的权限，则无法删除该对象。  
  
 <xref:Microsoft.AnalysisServices.RoleMember> 对象是通过以下方式创建的：向角色的成员集合添加一个用户，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Role> 对象更新到服务器中。 只允许服务器管理员或数据库管理员创建角色。 必须先将 <xref:Microsoft.AnalysisServices.Role> 对象更新到服务器中，才允许该服务器的任何成员使用已对其授予用户权限的所有对象。  
  
 若要删除 <xref:Microsoft.AnalysisServices.RoleMember> 对象，则必须使用集合的 Remove 方法从集合中删除该对象，然后使用 Update 方法更新角色。  
  
 有关可用于这些对象的方法和属性的详细信息，请参阅 <xref:Microsoft.AnalysisServices.Role> 中的 <xref:Microsoft.AnalysisServices.RoleMember> 和 <xref:Microsoft.AnalysisServices>。  
  
##  <a name="Permissions"></a> 权限对象  
 <xref:Microsoft.AnalysisServices.Permission> 对象是通过以下方式创建的：将其添加到对象的权限集合，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Permission> 对象更新到服务器中。  
  
 若要删除 <xref:Microsoft.AnalysisServices.Permission> 对象，必须使用该对象的 Drop 方法来删除。 在权限集合中使用 Remove 方法只会让您在应用程序中看不到该权限，而不会从服务器中删除 <xref:Microsoft.AnalysisServices.Permission> 对象。 如果存在任何与该角色关联的权限，则无法删除该角色。  
  
 有关可用方法和属性的详细信息，请参阅<xref:Microsoft.AnalysisServices.Permission>中<xref:Microsoft.AnalysisServices>。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices>   
 [编程 AMO 安全对象](programming-amo-security-objects.md)   
 [权限和访问权限&#40;Analysis Services-多维数据&#41;](https://msdn.microsoft.com/library/ms174786(v=sql.120).aspx)   
 [引入 AMO 类](amo-classes-introduction.md)   
 [逻辑体系结构&#40;Analysis Services-多维数据&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象&#40;Analysis Services-多维数据&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  