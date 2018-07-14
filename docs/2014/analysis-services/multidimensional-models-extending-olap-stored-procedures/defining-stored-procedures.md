---
title: 定义存储的过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d6f947e454901bbaf251488b6c57866f4c6bc55c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254929"
---
# <a name="defining-stored-procedures"></a>定义存储过程
  可以使用存储的过程调用中的外部例程[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 您可以在任何公共语言运行时 (CLR) 语言（例如 C、C++、C#、Visual Basic 或 Visual Basic .NET）中编写由存储过程调用的外部例程。 存储过程可以一次创建并从许多上下文中进行调用，例如其他存储过程、计算度量值或客户端应用程序。 程序集通过使通用代码可以一次开发并存储在单个位置中，简化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库开发和实现。 存储过程可用来向应用程序中添加 MDX 的本机功能未提供的商业功能。  
  
 本节提供了解、设计和实现存储过程所需的信息。  
  
|主题|Description|  
|-----------|-----------------|  
|[设计存储过程](../multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|介绍如何设计用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的程序集。|  
|[创建存储过程](creating-stored-procedures.md)|介绍如何为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建程序集。|  
|[调用存储过程](calling-stored-procedures.md)|提供有关如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用程序集的信息。|  
|[访问存储过程中的查询上下文](accessing-query-context-in-stored-procedures.md)|介绍如何使用程序集访问作用域和上下文信息。|  
|[设置存储过程的安全性](setting-security-for-stored-procedures.md)|介绍如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中配置程序集的安全性。|  
|[调试存储过程](debugging-stored-procedures.md)|介绍了如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中调试程序集。|  
  
## <a name="see-also"></a>请参阅  
 [多维模型程序集管理](../multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
