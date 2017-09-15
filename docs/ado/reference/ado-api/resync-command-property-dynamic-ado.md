---
title: "重新同步命令属性的动态 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cfa4fee83eef9c17a7dfb1eae6dbad64be2c98ce
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="resync-command-property-dynamic-ado"></a>重新同步命令属性的动态 (ADO)
指定用户提供的命令字符串[重新同步](../../../ado/reference/ado-api/resync-method.md)要刷新中名为的表中的数据的方法问题[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)动态属性。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值即命令字符串。  
  
## <a name="remarks"></a>注释  
 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象是在多个基表上执行联接操作的结果。 取决于受影响的行*AffectRecords*参数[重新同步](../../../ado/reference/ado-api/resync-method.md)方法。 标准**重新同步**如果执行方法[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和**重新同步命令**未设置属性。  
  
 命令字符串**重新同步命令**属性为参数化的命令或唯一标识要刷新的行的存储的过程并返回单个行的行包含相同数量和列顺序刷新。 该命令字符串包含在每个主键列的参数**唯一表**; 否则为返回运行时错误。 参数自动填写要刷新的行中的主键值。  
  
 下面是基于 SQL 的两个示例：  
  
 1\) **记录集**定义的命令：  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 **重新同步命令**属性设置为：  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **唯一表**是*订单*和其 primary key， *OrderID*，进行参数化。 嵌套 select 提供以编程方式确保按原始命令返回相同数量和顺序的列的简单方法。  
  
 2\) **记录集**由存储过程定义：  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **重新同步**方法应执行以下存储的过程：  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 **重新同步命令**属性设置为：  
  
```  
"{call CustordersResync (?)}"  
```  
  
 同样，**唯一表**是*订单*和其 primary key， *OrderID*，进行参数化。  
  
 **重新同步命令**动态属性追加到**记录集**对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
