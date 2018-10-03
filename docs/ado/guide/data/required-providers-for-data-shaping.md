---
title: 必需的提供程序数据整理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 482139f8aa3dc42bbd17593b58fcc8510f1fc9a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713835"
---
# <a name="required-providers-for-data-shaping"></a>数据整理所需的提供程序
数据整理通常需要两个提供程序。 服务提供商，[适用于 OLE DB Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)，提供数据整理功能和数据提供程序，如 SQL Server 的 OLE DB 访问接口，提供行的数据来填充形状[记录集](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 服务提供程序 (MSDataShape) 的名称可以指定的值为[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性或连接字符串关键字"提供程序 = MSDataShape;"。  
  
 数据提供程序的名称可以指定的值为**数据提供程序**动态属性，它将添加到**连接**对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合数据整理服务的 OLE DB 或连接字符串关键字"**数据提供程序 = * * * 提供程序*"。  
  
 如果没有数据提供程序，则需要**记录集**未填充 (例如，如下所示虚构**记录集**其中使用 NEW 关键字创建的列)。 在这种情况下，指定"**数据提供程序 =** none;"。  
  
## <a name="example"></a>示例  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
