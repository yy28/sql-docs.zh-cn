---
title: ADO 动态属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71396a071a42d7dd40a6537a2834541aab2b6bad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921097"
---
# <a name="ado-dynamic-properties"></a>ADO 动态属性
可以将动态属性添加到[连接](../../../ado/reference/ado-api/connection-object-ado.md)、[命令](../../../ado/reference/ado-api/command-object-ado.md)或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的[properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 这些属性的来源是数据提供程序，例如[用于 SQL Server 的 OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)或服务提供程序（如[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)）。 有关特定动态属性的详细信息，请参阅相应的数据提供程序或服务提供程序文档。  
  
 [Ado 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)在每个标准 OLE DB 提供程序动态属性的 ADO 和 OLE DB 名称之间提供交叉引用。  
  
 以下动态属性特别有趣，还在前面提到的源中进行了介绍。 以下列表的 ADO 帮助主题中记录了 ADO 的特殊功能。  
  
|||  
|-|-|  
|[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指定是否应在此字段上创建索引。|  
|[提示](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|指定 OLE DB 提供程序是否应提示用户提供初始化信息。|  
|[调整名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|指定**记录集**对象的名称。|  
|[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|指定一个用户提供的命令字符串，重新**同步**方法发出此命令以刷新 "**唯一表**动态" 属性中命名的表中的数据。|  
|[唯一表、唯一架构、唯一目录](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**唯一表**指定允许更新、插入和删除的基表的名称。<br /><br /> **唯一架构**指定表所有者的架构或名称。<br /><br /> **唯一目录**指定包含表的数据库的目录或名称。|  
|[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|指定**UpdateBatch**方法是否后跟隐式重新**同步**方法操作，如果是，则为该操作的范围。|  
  
## <a name="see-also"></a>另请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 B： ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 对象和接口](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
