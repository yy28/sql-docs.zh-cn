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
manager: jroth
ms.openlocfilehash: 7345f75d43d302c71db91aefa9097a4d34e72d94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700964"
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
