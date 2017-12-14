---
title: "使用基于策略的管理方面 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05553cdc32533cb13899a2aee5b09c695e1d7547
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-policy-based-management-facets"></a>使用基于策略的管理方面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]基于策略的管理方面是一组与管理领域相关的逻辑属性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括几个预定义的方面。 例如，将默认关闭的功能定义为属性的外围应用配置器方面。  
  
 在管理许多类似的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境时，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的一个实例中配置一个方面，将该方面的状态复制到文件中，然后将该文件作为策略导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一个实例中。 将状态转换为策略后，可以将该策略应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他实例、实例对象、数据库或数据库对象。  
  
 本主题说明如何将方面状态复制到 XML 文件中。  
  
##  <a name="BeforeYouBegin"></a> 权限  
 本主题中的过程要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
## <a name="viewing-and-copying-facet-states"></a>查看和复制方面状态  
 [查看 SQL Server 对象的基于策略的管理方面](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [将基于策略的管理方面状态复制到 XML 文件中](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
