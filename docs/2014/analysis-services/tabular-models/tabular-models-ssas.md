---
title: 表格建模 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11a5a9332c7fa85fd6407523ffd9c7c48a2c0514
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198747"
---
# <a name="tabular-modeling-ssas-tabular"></a>表格建模（SSAS 表格）
  表格模型是 Analysis Services 中的内存中数据库。 使用最先进的压缩算法和多线程查询处理器，xVelocity 内存中分析引擎 (VertiPaq) 可通过报表客户端应用程序（如 Microsoft Excel 和 Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]）来快速访问表格模型对象和数据。  
  
 表格模型通过两种模式支持数据访问：缓存模式和 DirectQuery 模式。 在缓存模式中，可以集成多个源的数据，包括关系数据库、数据馈送和平面文本文件。 在 DirectQuery 模式中，可以绕开内存中模型，允许客户端应用程序直接在（SQL Server 关系）源上查询数据。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中使用新的表格模型项目模板创建表格模型。 您可以从多个源导入数据，然后通过添加关系、计算列、度量值、KPI 和层次结构来丰富模型。 然后可以将模型部署到客户端报告应用程序可以连接到的 Analysis Services 实例。 可以在 SQL Server Management Studio 中管理已部署的模型，就像管理多维模型一样。 还可以对它们进行分区以便优化处理，并使用基于角色的安全性保护行级数据安全。  
  
## <a name="in-this-section"></a>本节内容  
 [表格模型解决方案&#40;SSAS 表格&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
 [表格模型数据库&#40;SSAS 表格&#41;](tabular-model-databases-ssas-tabular.md)  
  
 [表格模型数据访问](tabular-model-data-access.md)  
  
  
