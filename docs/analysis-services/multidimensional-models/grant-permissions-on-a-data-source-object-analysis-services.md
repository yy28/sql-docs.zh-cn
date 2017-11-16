---
title: "授予对数据源对象 (Analysis Services) 的权限 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.datasources.f1
helpviewer_keywords:
- read/write permissions
- user access rights [Analysis Services], data sources
- security [Analysis Services], data sources
- connection strings [Analysis Services]
- data sources [Analysis Services], security
ms.assetid: b4e302d3-c93b-4383-aa4a-37d15c129830
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e64c0b5496352e1336046c4066de1f0cf625462
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-permissions-on-a-data-source-object-analysis-services"></a>授予数据源对象的权限 (Analysis Services)
  通常，大多数 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用户无需访问作为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目基础的数据源。 用户通常只查询 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的数据。 但是，在数据挖掘上下文中（如根据挖掘模型执行预测），用户必须将挖掘模型的已学习数据与用户提供的数据联接起来。 为了连接到包含用户提供数据的数据源，用户将使用包含 [OPENQUERY (DMX)](../../dmx/source-data-query-openquery.md) 或 [OPENROWSET (DMX)](../../dmx/source-data-query-openrowset.md) 子句的数据挖掘扩展插件 (DMX) 查询。  
  
 若要执行连接到数据源的 DMX 查询，用户必须能访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的数据源对象。 默认情况下，只有数据库管理员或服务器管理员具有访问数据源对象的权限。 这意味着，除非管理员授予权限，否则用户将不能访问数据源对象。  
  
> [!IMPORTANT]  
>  出于安全方面的考虑，系统禁止在 OPENROWSET 子句中使用公开连接字符串来提交 DMX 查询。  
  
## <a name="set-read-permissions-to-a-data-source"></a>设置对数据源的读取权限  
 可以使数据库角色无权访问数据源对象，也可以授予其读取权限。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中展开相应数据库的“角色”，然后单击某个数据库角色（或创建一个新的数据库角色）。  
  
2.  在“数据源访问”窗格  ，找到“数据源”列表中的数据源对象  ，然后在该数据源的“访问”列表  中选择“读”  。 如果此选项不可用，请检查“常规”  面板，以查看是否已选择“完全控制”。 “完全控制”已在提供权限，你不能覆盖数据源上的权限。  
  
## <a name="working-with-the-connection-string-used-by-a-data-source-object"></a>使用数据源对象使用的连接字符串  
 数据源对象包括用于连接到基础数据源的连接字符串。 此连接字符串可以指定以下内容之一：  
  
-   **指定用户名和密码**  
  
     如果数据源对象使用的连接字符串指定了用户名和密码，则可以创建多个数据源对象，每个对象都有不同的用户帐户。 通过创建多个数据源对象，可允许用户访问某些数据源对象，并可阻止用户访问其他数据源对象。 其他这些数据源对象可由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自身使用，用于处理对象（如多维数据集和挖掘模型）。  
  
-   **指定 Windows 身份验证**  
  
     如果数据源对象使用的连接字符串指定了 Windows 身份验证，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 必须能够模拟客户端。 如果数据源在远程计算机上，两台计算机必须使用 Kerberos 身份验证建立模拟信任，否则查询一般会失败。 有关详细信息，请参阅 [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) 。  
  
     如果客户端不允许模拟（通过 OLE DB 和其他客户端组件中的“Impersonation Level”属性），则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将尝试匿名连接到基础数据源（大多数数据源不接受匿名连接）。 糯米连接到远程数据源很少成功，这是因为大多数数据源不接受匿名连接。）  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [连接字符串属性 &#40;Analysis Services &#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)   
 [Analysis Services 支持的身份验证方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [授予维度数据 &#40; 的自定义访问权限Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [授予多维数据集或模型权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [授予单元数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  

