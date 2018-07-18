---
title: ADO 动态属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.service: ''
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5aa6d237b16c6ac24c0e921d51f19a26c36e3bbe
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35275446"
---
# <a name="ado-dynamic-properties"></a>ADO 动态属性
可以将动态属性添加到[属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[命令](../../../ado/reference/ado-api/command-object-ado.md)，或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 这些属性的源是哪种数据提供程序，如[OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，或服务提供程序，如[Microsoft 游标服务用于 OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)。 引用适当的数据提供程序或服务提供程序文档，了解有关特定的动态属性的详细信息。  
  
 [ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)提供每个标准的 OLE DB 提供程序动态属性的 ADO 和 OLE DB 名称之间的交叉引用。  
  
 以下的动态属性是特别值得关注，并且还都记录在前面提到的源。 以下列表中的 ADO 帮助主题中描述了用 ADO 的特殊功能。  
  
|||  
|-|-|  
|[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指定是否应在此字段创建索引。|  
|[提示符](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|指定的 OLE DB 访问接口是否应提示用户输入的初始化信息。|  
|[重新调整形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|指定的名称**记录集**对象。|  
|[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|指定用户提供的命令字符串**重新同步**要刷新中名为的表中的数据的方法问题**唯一表**动态属性。|  
|[唯一表、 唯一的架构、 唯一的目录](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**唯一表**指定的更新、 插入和删除允许在其基础表的名称。<br /><br /> **唯一架构**指定架构或表的所有者的名称。<br /><br /> **唯一的目录**指定的目录或包含的表的数据库名称。|  
|[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|指定是否**UpdateBatch**方法后跟一种隐式**重新同步**方法操作，如果是，该操作的作用域。|  
  
## <a name="see-also"></a>请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 b: ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 对象和接口](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
