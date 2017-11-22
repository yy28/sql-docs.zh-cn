---
title: "访问中的查询上下文存储过程 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d2a53ac7fb66ded14a7e79dee881755fc7ecd45e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="accessing-query-context-in-stored-procedures"></a>访问存储过程中的查询上下文
  存储过程的执行上下文中有可用的存储过程作为代码**上下文**ADOMD.NET 服务器对象模型的对象。 这是只读上下文，存储过程不能修改它。 此对象的以下属性可用。  
  
|属性|类型|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|多维数据集|当前查询上下文的多维数据集。|  
|**CurrentDatabaseName**|字符串|当前数据库的标识符。|  
|**CurrentConnection**|连接|对当前上下文中连接对象的引用。|  
|**传递**|Integer|当前上下文的传递号。|  
  
 **上下文**在存储过程中使用的多维表达式 (MDX) 对象模型时存在的对象。 而在客户端上使用 MDX 对象模型时，该对象不可用。 **上下文**未显式传递到或存储过程返回的对象。 它只在存储过程的执行期间可用。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
