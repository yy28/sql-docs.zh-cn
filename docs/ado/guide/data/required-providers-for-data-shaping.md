---
title: "必需的提供程序数据成型 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2dc7048ea3442a77f6aadf7d7b1868c2ac9d833
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="required-providers-for-data-shaping"></a>所需的提供程序，供你调整数据
数据成型通常需要两个提供程序。 服务提供商[用于 OLE DB 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)，提供调整功能和数据提供程序，如 OLE DB Provider for SQL Server 的数据，提供要填充形状的数据行[记录集](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 服务提供程序 (MSDataShape) 的名称可以指定的值为[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性或连接字符串关键字"提供程序 = MSDataShape;"。  
  
 数据提供程序的名称可以指定的值为**数据提供程序**动态属性，添加到**连接**对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合数据调整服务对于 OLE DB 或连接字符串关键字"**数据提供程序 =***提供程序*"。  
  
 如果任何数据提供程序，则需要**记录集**不填充 (例如，如下所示虚构**记录集**其中用新关键字创建列)。 在这种情况下，指定"**数据提供程序 =**none;"。  
  
## <a name="example"></a>示例  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>另请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)
