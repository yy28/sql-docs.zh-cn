---
title: 使用 AddNew 添加记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f6bad9a8f0d74a81d02ce64c78d7a91ddc0fa8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926285"
---
# <a name="adding-records-using-addnew-method"></a>使用 AddNew 方法添加记录
这是**AddNew**方法的基本语法：

 *记录集*。AddNew *FieldList*，*值*

 *FieldList*和*Values*参数是可选的。 *FieldList*是新记录中字段的单个名称或名称数组或序号位置数组。

 *Values*参数是新记录中的字段的单个值或值数组。

 通常，当你要添加单个记录时，将调用不带任何参数的**AddNew**方法。 具体来说，您将调用**AddNew**;设置新记录中每个字段的**值**;然后调用**Update**或**UpdateBatch**，或同时调用两者。 您可以通过使用带有**adAddNew**枚举常量的 "**支持**" 属性，确保您的**记录集**支持添加新记录。

 下面的代码使用此方法将新的货主添加到示例**记录集中**。 SQL Server 自动提供 "ShipperID" 字段值。 因此，该代码不会尝试为新记录提供字段值。

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>备注
 因为此代码在批处理模式下将断开连接的**记录集**与客户端游标一起使用，所以必须使用新的**连接**对象将**记录集**重新连接到数据源，然后才能调用**UpdateBatch**方法将更改发布到数据库。 使用新的函数**GetNewConnection**可以轻松完成此操作。
