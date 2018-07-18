---
title: ADO 对象和集合 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d8b1967071b5dc420577ecbee3f1b124d917057
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271376"
---
# <a name="ado-objects-and-collections"></a>ADO 对象和集合
ADO 由以下九个对象和四个集合组成。  
  
|对象或集合|Description|  
|--------------------------|-----------------|  
|**连接**对象|表示与某一数据源的唯一会话。 对于客户端/服务器数据库系统，它可能等效于与服务器的实际网络连接。 具体取决于提供程序、 一些集合、 方法或属性的支持的功能**连接**对象可能不可用。|  
|**Command** 对象|用于定义特定的命令，例如 SQL 查询，用于对数据源运行。|  
|**记录集**对象|表示整个组记录从基表或执行命令的结果。 所有**记录集**对象包含的记录 （行） 和字段 （列）。|  
|**记录**对象|表示单个行的数据，从**记录集**或从提供程序。 此记录可表示的数据库记录或某些其他类型的对象，如文件或目录，根据你的提供商。|  
|**流**对象|表示二进制或文本数据的流。 例如，XML 文档可以加载到一个流以便输入或从某些提供程序返回作为查询的结果的命令。 A**流**对象可以用于操作字段或包含这些数据流的数据的记录。|  
|**参数**对象|表示参数或参数与关联**命令**基于参数化的查询或存储的过程的对象。|  
|**字段**对象|表示对类型为通用数据类型的数据列。 每个**字段**对象中的列对应**记录集**。|  
|**属性**对象|表示由提供程序定义的 ADO 对象的特征。 ADO 对象有两种类型的属性： 内置和动态。 内置属性是在 ADO 和任何新对象可立即用于实现这些属性。 **属性**对象是由基础提供程序定义的动态属性的容器。|  
|**Error** 对象|包含有关适用于涉及提供程序的单个操作的数据访问错误的详细信息。|  
|**字段**集合|包含所有**字段**的对象**记录集**或**记录**对象。|  
|**属性**集合|包含所有**属性**对象的特定实例的对象。|  
|**参数**集合|包含所有**参数**的对象**命令**对象。|  
|**错误**集合|包含所有**错误**到单个提供程序相关的失败的响应中创建的对象。|  
  
## <a name="see-also"></a>请参阅  
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)
