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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926285"
---
# <a name="adding-records-using-addnew-method"></a>添加记录使用 AddNew 方法
这是基本的语法**AddNew**方法：

 *记录集*。AddNew *FieldList*，*值*

 *FieldList*并*值*参数是可选的。 *FieldList*为单个名称或名称的数组或新记录中字段的序号位置。

 *值*参数为单个值或数组的新记录中字段的值。

 通常情况下，当你想要添加一条记录，您将调用**AddNew**不带任何参数的方法。 具体而言，将调用**AddNew**; set**值**每个字段中的新记录;，然后调用**更新**或者**UpdateBatch**，或两者。 可确保你**记录集**支持通过添加新记录**支持**具有属性**adAddNew**枚举的常数。

 以下代码使用此技术的示例添加新的发货方**记录集**。 SQL Server 会自动提供 ShipperID 字段值。 因此，代码不会尝试提供新的记录的字段值。

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
 因为此代码使用已断开连接**记录集**利用在批处理模式下客户端游标，必须重新连接**记录集**到具有一个新的数据源**连接**对象，然后可以调用才能**UpdateBatch**方法来更改发布到数据库。 这轻松地通过使用新的函数**GetNewConnection**。
