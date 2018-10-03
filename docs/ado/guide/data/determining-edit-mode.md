---
title: 确定编辑模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e638cda03d7dc0f0bd580c3ca29c126568d1595a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705235"
---
# <a name="determining-edit-mode"></a>确定编辑模式
ADO 维护一个与当前记录相关联的编辑缓冲区。 **EditMode**属性指示是否进行了更改到此缓冲区或是否已创建一个新的记录。 使用**EditMode**来确定当前记录的编辑状态。 您可以测试挂起的更改被中断编辑过程并确定是否需要使用**更新**或**CancelUpdate**方法。  
  
 **EditMode**返回的一个**EditModeEnum**常量下, 表中列出。  
  
|常量|Description|  
|--------------|-----------------|  
|**adEditNone**|指示不编辑操作正在进行中。|  
|**adEditInProgress**|指示当前记录中的数据已修改但尚未保存。|  
|**adEditAdd**|指示**AddNew**已调用方法，并且复制缓冲区中的当前记录是尚未保存到数据库的新记录。|  
|**adEditDelete**|指示当前记录已被删除。|  
  
 **EditMode**没有当前记录的情况下，才可以返回有效的值。 **EditMode**将返回一个错误，如果**BOF**或**EOF**是**True** ，或者删除当前记录。
