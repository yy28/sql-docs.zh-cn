---
title: 在即时和批处理模式下使用 AddNew |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 265b1dcd3cdc1aa7f18f0ca54dc2cf54df2da158
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923628"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>以即时和批处理模式使用 AddNew
**AddNew**方法的行为取决于**记录集**对象的更新模式，以及是否传递*FieldList*和*Values*参数。  
  
 在立即更新模式下（在调用**update**方法后，提供程序将更改写入基础数据源），调用不带参数的**AddNew**方法会将**EditMode**属性设置为**adEditAdd。** 提供程序在本地缓存任何字段值更改。 调用**Update**方法会将新记录发送到数据库，并将**EditMode**属性重置为**adEditNone。** 如果传递*FieldList*和*VALUES*参数，ADO 会立即将新记录发送到数据库（无需**更新**调用）;**EditMode**属性值不会更改（**adEditNone**）。  
  
 在批处理更新模式中，如果调用不带参数的**AddNew**方法，则将**EditMode**属性设置为**adEditAdd**。 提供程序在本地缓存任何字段值更改。 调用**Update**方法会将新记录添加到当前**记录集**，并将**EditMode**属性重置为**adEditNone**，但在调用**UpdateBatch**方法之前，提供程序不会将更改发布到基础数据库。 如果传递了*FieldList*和*Values*参数，则 ADO 会将新记录发送到提供程序以用于缓存中的存储;需要调用**UpdateBatch**方法将新记录发布到基础数据库。 有关**Update**和**UpdateBatch**的详细信息，请参阅[更新和保留数据](../../../ado/guide/data/updating-and-persisting-data.md)。
