---
title: "确定编辑模式 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ca4098a61984e009a2874fdca55d898938ce702d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="determining-edit-mode"></a>确定编辑模式
ADO 维护一个与当前记录关联的编辑缓冲区。 **EditMode**属性指示是否进行了更改到此缓冲区，或是否已创建一条新记录。 使用**EditMode**来确定当前记录的编辑状态。 你可以测试挂起的更改被中断编辑过程并确定是否需要使用**更新**或**正在执行**方法。  
  
 **EditMode**返回之一**EditModeEnum**常量下, 表中列出。  
  
|常量|Description|  
|--------------|-----------------|  
|**adEditNone**|指示任何编辑操作正在进行。|  
|**adEditInProgress**|指示当前记录中的数据已修改但尚未保存。|  
|**adEditAdd**|指示**AddNew**已调用方法，并且复制缓冲区中的当前记录是一条新记录，不保存到数据库。|  
|**adEditDelete**|指示当前记录已被删除。|  
  
 **EditMode**可以返回有效的值，只有在当前记录。 **EditMode**将返回错误，如果**BOF**或**EOF**是**True**或如果已删除该当前记录。

