---
title: 访问中的查询上下文存储过程 |Microsoft 文档
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
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ef60683eb410f0db5ba9e8d38ac227ca22dd9159
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024929"
---
# <a name="accessing-query-context-in-stored-procedures"></a>访问存储过程中的查询上下文
  存储过程的执行上下文可以作为 ADOMD.NET 服务器对象模型的 `Context` 对象出现在存储过程代码中。 这是只读上下文，存储过程不能修改它。 此对象的以下属性可用。  
  
|“属性”|类型|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|多维数据集|当前查询上下文的多维数据集。|  
|**CurrentDatabaseName**|String|当前数据库的标识符。|  
|**CurrentConnection**|连接|对当前上下文中连接对象的引用。|  
|**传递**|Integer|当前上下文的传递号。|  
  
 在存储过程中使用多维表达式 (MDX) 对象模型时，将会存在 `Context` 对象。 而在客户端上使用 MDX 对象模型时，该对象不可用。 `Context` 对象不会显式传递给存储过程，也不会被存储过程返回。 它只在存储过程的执行期间可用。  
  
## <a name="see-also"></a>请参阅  
 [多维模型程序集管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储过程](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  