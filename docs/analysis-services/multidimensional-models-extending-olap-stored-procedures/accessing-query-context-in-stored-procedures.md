---
title: 访问中的查询上下文存储过程 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a2d0787aa76107b30b91558830d98f068a7301e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="accessing-query-context-in-stored-procedures"></a>访问存储过程中的查询上下文
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [定义存储的过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
