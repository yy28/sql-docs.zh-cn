---
title: "构造分层记录集 |Microsoft 文档"
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
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f8b01b8cd08c46f641fbd713f4acbdeca53db5c6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="fabricating-hierarchical-recordsets"></a>构造分层记录集
下面的示例演示如何使用调整语法来定义为父、 子节点和孙级的列的数据生成分层记录集而无需基础数据源**记录集**。  
  
 生成一种分层**记录集**，必须指定[用于 OLE DB （ADO 服务提供程序） 的 Microsoft 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)(MSDataShape)，并可以指定无数据提供程序值连接字符串参数[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 有关详细信息，请参阅[所需的提供程序数据成型](../../../ado/guide/data/required-providers-for-data-shaping.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [访问在分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [所需的提供程序，供你调整数据](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [形状 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)
