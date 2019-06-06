---
title: 构造分层记录集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5dc84c5bacca8951576e572b90fa28a8408e48d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700722"
---
# <a name="fabricating-hierarchical-recordsets"></a>构造分层记录集
下面的示例演示如何通过使用数据整理语法来定义列的父级、 子级和孙级编制分层记录集而无需基础数据源**记录集**。  
  
 创建一种分层**记录集**，必须指定[适用于 OLE DB （ADO 服务提供商） 的 Microsoft Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)(MSDataShape)，并可以指定数据提供程序值 NONE 中连接字符串参数[开放](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 有关详细信息，请参阅[将提供程序所需的数据整理](../../../ado/guide/data/required-providers-for-data-shaping.md)。  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 只要**记录集**已制造，它可以填充、 操作，或保存到文件。  
  
## <a name="see-also"></a>请参阅  
 [访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [数据整理所需的提供程序](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
