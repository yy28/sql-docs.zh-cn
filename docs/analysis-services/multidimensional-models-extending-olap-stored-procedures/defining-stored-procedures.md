---
title: 定义存储的过程 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54b14cd5ee54edab4508c06c55e5815bfeab934f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209380"
---
# <a name="defining-stored-procedures"></a>定义存储过程
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以使用存储的过程调用中的外部例程[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 您可以在任何公共语言运行时 (CLR) 语言（例如 C、C++、C#、Visual Basic 或 Visual Basic .NET）中编写由存储过程调用的外部例程。 存储过程可以一次创建并从许多上下文中进行调用，例如其他存储过程、计算度量值或客户端应用程序。 程序集通过使通用代码可以一次开发并存储在单个位置中，简化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库开发和实现。 存储过程可用来向应用程序中添加 MDX 的本机功能未提供的商业功能。  
  
 本节提供了解、设计和实现存储过程所需的信息。  
  
|主题|描述|  
|-----------|-----------------|  
|[设计存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|介绍如何设计用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的程序集。|  
|[创建存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|介绍如何为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建程序集。|  
|[调用存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|提供有关如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用程序集的信息。|  
|[访问存储过程中的查询上下文](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|介绍如何使用程序集访问作用域和上下文信息。|  
|[设置存储过程的安全性](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|介绍如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中配置程序集的安全性。|  
|[调试存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|介绍了如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中调试程序集。|  
  
## <a name="see-also"></a>请参阅  
 [多维模型程序集管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
