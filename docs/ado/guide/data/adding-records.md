---
title: 添加记录 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aeaf7182685ff0b7621d208ba684976da7bf07bd
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="adding-records-to-a-recordset"></a>将记录添加到记录集
使用**AddNew**方法创建并初始化新记录中的现有**记录集**。 你可以使用**支持**方法替换**CursorOptionEnum**值**adAddNew**以验证是否可以将记录添加到当前**记录集**对象。

 调用后**AddNew**方法，新的记录将成为当前记录和调用方法后仍当前**更新**方法。 如果**记录集**对象不支持书签，你可能无法访问新的记录，一旦您移动到另一条记录。 因此，具体取决于游标类型，你可能需要调用**Requery**方法，以便可以访问新的记录。

 如果调用**AddNew** ADO 时编辑当前记录或添加新记录时，调用**更新**方法来保存任何更改，然后创建新的记录。

 本部分包含以下主题。

-   [使用 AddNew 添加记录](../../../ado/guide/data/adding-records-using-addnew.md)

-   [添加多个字段](../../../ado/guide/data/adding-multiple-fields.md)

-   [确定编辑模式](../../../ado/guide/data/determining-edit-mode.md)

-   [以即时和批处理模式使用 AddNew](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
