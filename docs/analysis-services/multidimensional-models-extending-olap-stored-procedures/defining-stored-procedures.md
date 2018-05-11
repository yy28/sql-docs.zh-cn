---
title: 定义存储的过程 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a251da65ced87835b6de50d71bd60658db17fd9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="defining-stored-procedures"></a>定义存储过程
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  你可以使用存储的过程调用从外部例程[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 您可以在任何公共语言运行时 (CLR) 语言（例如 C、C++、C#、Visual Basic 或 Visual Basic .NET）中编写由存储过程调用的外部例程。 存储过程可以一次创建并从许多上下文中进行调用，例如其他存储过程、计算度量值或客户端应用程序。 程序集通过使通用代码可以一次开发并存储在单个位置中，简化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库开发和实现。 存储过程可用来向应用程序中添加 MDX 的本机功能未提供的商业功能。  
  
 本节提供了解、设计和实现存储过程所需的信息。  
  
|主题|Description|  
|-----------|-----------------|  
|[设计存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|介绍如何设计用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的程序集。|  
|[创建存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|介绍如何为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建程序集。|  
|[调用存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|提供有关如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用程序集的信息。|  
|[访问存储过程中的查询上下文](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|介绍如何使用程序集访问作用域和上下文信息。|  
|[设置存储过程的安全性](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|介绍如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中配置程序集的安全性。|  
|[调试存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|介绍了如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中调试程序集。|  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
