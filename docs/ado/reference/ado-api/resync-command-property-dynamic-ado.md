---
title: 重新同步命令属性-动态（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: rothja
ms.author: jroth
ms.openlocfilehash: 916afef294a76e62702dbbd7cc413a0540484f62
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756480"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command 属性 - 动态 (ADO)
指定一个用户提供的命令字符串，重新[同步](../../../ado/reference/ado-api/resync-method.md)方法发出此命令以刷新 "[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)动态" 属性中命名的表中的数据。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**字符串**值，该值为命令字符串。  
  
## <a name="remarks"></a>备注  
 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象是对多个基表执行的联接操作的结果。 受影响的行依赖于[Resync](../../../ado/reference/ado-api/resync-method.md)方法的*AffectRecords*参数。 如果未设置[Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和**Resync 命令**属性，则执行标准的重新**同步**方法。  
  
 **Resync command**属性的命令字符串是一个参数化命令或存储过程，用于唯一标识要刷新的行，并返回包含与要刷新的行相同的列数和顺序的单个行。 命令字符串为**唯一表**中的每个主键列包含一个参数;否则，将返回运行时错误。 将自动用要刷新的行中的主键值填充参数。  
  
 下面是基于 SQL 的两个示例：  
  
 1 \) 通过命令定义**记录集**：  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 重新**同步命令**属性设置为：  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **唯一表**为*Orders* *，其*主键是参数化的。 子选择提供了一种简单的方法，可通过编程方式确保按原始命令返回相同的列数和列顺序。  
  
 2 \) **记录集**由存储过程定义：  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **Resync**方法应执行以下存储过程：  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 重新**同步命令**属性设置为：  
  
```  
"{call CustordersResync (?)}"  
```  
  
 同样，**唯一表**是*订单*，其主键 "订单*id*" 已参数化。  
  
 当[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**AdUseClient**时， **Resync 命令**是追加到**Recordset**对象[Properties](../../../ado/reference/ado-api/properties-collection-ado.md) collection 的动态属性。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
