---
title: ADO 对象和集合 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5743e04b402302cc53b7694d8160edfb11769e0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783875"
---
# <a name="ado-objects-and-collections"></a>ADO 对象和集合
ADO 由以下九个对象和四个集合组成。  
  
|对象或集合|Description|  
|--------------------------|-----------------|  
|**连接**对象|表示与某一数据源的唯一会话。 对于客户端/服务器数据库系统，它可能与实际的网络连接到服务器。 具体取决于提供程序、 一些集合、 方法或属性的支持的功能**连接**对象可能不可用。|  
|**Command** 对象|用于定义特定的命令，例如用于对数据源运行的 SQL 查询。|  
|**记录集**对象|表示整个记录集的基础表或执行命令的结果中。 所有**记录集**对象包含的记录 （行） 和字段 （列）。|  
|**记录**对象|表示的数据，即从一行**记录集**或从提供程序。 此记录可表示的数据库记录或某些其他类型的对象，例如文件或目录中，根据您的提供程序。|  
|**Stream**对象|表示二进制或文本数据的流。 例如，XML 文档可以加载到一个流以便输入或从某些提供程序返回作为查询的结果的命令。 一个**Stream**对象可用于操作的字段或包含这些流数据的记录。|  
|**参数**对象|表示参数或参数与相关联**命令**基于参数化的查询或存储的过程的对象。|  
|**字段**对象|表示与常见的数据类型的数据的列。 每个**字段**对象中的列对应**记录集**。|  
|**属性**对象|表示由提供程序定义的 ADO 对象的特征。 ADO 对象具有两种类型的属性： 内置和动态。 内置属性是在 ADO 和任何新的对象可以立即实现这些属性。 **属性**对象是由基础提供程序定义的动态属性的容器。|  
|**Error** 对象|包含有关适用于单个操作涉及该提供程序的数据访问错误的详细信息。|  
|**字段**集合|包含所有**字段**的对象**记录集**或**记录**对象。|  
|**属性**集合|包含所有**属性**对象的特定实例的对象。|  
|**参数**集合|包含所有**参数**的对象**命令**对象。|  
|**错误**集合|包含所有**错误**到单个提供程序相关的失败的响应中创建的对象。|  
  
## <a name="see-also"></a>请参阅  
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)
