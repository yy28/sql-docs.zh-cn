---
title: "添加记录使用 AddNew |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92bbc404985ebbb49c4e654efd5a7f54198d35ab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="adding-records-using-addnew-method"></a>添加记录使用 AddNew 方法
这是基本语法的**AddNew**方法：

 *记录集*。AddNew *FieldList*，*值*

 *FieldList*和*值*参数是可选的。 *FieldList*是单个名称或名称的数组或新记录中的字段的序号位置。

 *值*参数是单个值或数组的新记录中的字段的值。

 通常情况下，当你想要添加的单个记录，你将调用**AddNew**不带任何参数的方法。 具体而言，将调用**AddNew**; 设置**值**每个字段中的新记录;，然后调用**更新**或**UpdateBatch**，或两者。 可以确保你**记录集**支持通过添加新记录**支持**具有属性**adAddNew**枚举的常数。

 下面的代码使用此方法的示例中添加新发货方**记录集**。 SQL Server 会自动提供 ShipperID 字段值。 因此，代码不会尝试提供新的记录的字段值。

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

## <a name="remarks"></a>注释
 因为此代码使用断开连接**记录集**与客户端游标在批处理模式下，你必须重新连接**记录集**到具有新的数据源**连接**对象，然后你可以调用**UpdateBatch**方法发布到数据库的更改。 轻松地完成此操作通过使用新函数**GetNewConnection**。

