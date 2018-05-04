---
title: 接收多个记录集 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a603e1c5f3498daa6140915be5d05494b1b968f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="receiving-multiple-recordsets"></a>接收多个记录集
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支持返回多个**记录集**对象为单个命令包含多个 SQL 语句，一个**记录集**每个 SQL 语句。 顺序**记录集**将返回遵循在其中的 SQL 语句放置在命令文本中的顺序。  
  
 Microsoft OLE DB Provider for SQL Server 的命令包含一个 COMPUTE 子句时，还将多个结果集返回到 ADO。 例如，包含以下 SQL 语句的命令会返回结果，在两个**记录集**对象： 一个用于行集 (*ProductID*， *ProductName*，*UnitPrice*)，另一个用于表中的所有产品的平均价格。  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 你可以使用**Recordset.NextRecordset**方法来枚举两个对象。  
  
 有关详细信息，请参阅[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md)。
