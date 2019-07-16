---
title: 使用 AddNew 以即时和批处理模式 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923628"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>以即时和批处理模式使用 AddNew
行为**AddNew**上的更新模式的方法取决于**记录集**对象和是否传递*FieldList*和*值*自变量。  
  
 在立即更新模式 (在其中提供程序将更改写入到基础数据源后，调用**更新**方法)，则调用**AddNew**方法无参数集**EditMode**属性设置为**adEditAdd。** 提供程序将任何字段值更改在本地缓存。 调用**更新**方法将发布到数据库的新记录，并将重置**EditMode**属性设置为**adEditNone。** 如果传递*FieldList*并*值*自变量，ADO 立即发布到数据库的新记录 (没有**更新**才需要调用); **EditMode**属性值不会更改 (**adEditNone**)。  
  
 在批更新模式下，调用**AddNew**方法，而参数集**EditMode**属性设置为**adEditAdd**。 提供程序将任何字段值更改在本地缓存。 调用**更新**方法将新记录添加到当前**记录集**并重置**EditMode**属性设置为**adEditNone**，但提供程序不会不将更改发布到基础数据库之前调用**UpdateBatch**方法。 如果传递*FieldList*和*值*自变量，ADO 将新记录发送到缓存中存储的提供程序; 您需要调用**UpdateBatch**要发布的新方法记录到基础数据库。 有关详细信息**更新**并**UpdateBatch**，请参阅[更新和保存数据](../../../ado/guide/data/updating-and-persisting-data.md)。
