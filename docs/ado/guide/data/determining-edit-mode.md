---
description: 确定编辑模式
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 788a91fc3de259210a5f2756f148161fbb90308e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453499"
---
# <a name="determining-edit-mode"></a>确定编辑模式
ADO 维护与当前记录相关联的编辑缓冲区。 **EditMode**属性指示是否已对此缓冲区进行了更改或者是否已创建新记录。 使用 **EditMode** 确定当前记录的编辑状态。 如果编辑进程已中断并确定是否需要使用 **Update** 或 **CancelUpdate** 方法，则可以测试挂起的更改。  
  
 **EditMode** 返回下表中列出的一个 **EditModeEnum** 常量。  
  
|返回的常量|描述|  
|--------------|-----------------|  
|**adEditNone**|指示没有正在进行的编辑操作。|  
|**adEditInProgress**|指示当前记录中的数据已修改但未保存。|  
|**adEditAdd**|指示已调用 **AddNew** 方法，并且复制缓冲区中的当前记录是尚未保存到数据库中的新记录。|  
|**adEditDelete**|指示当前记录已被删除。|  
  
 仅当存在当前记录时， **EditMode**才可以返回有效的值。 如果**BOF**或**EOF**为**True**或当前记录已被删除，则**EditMode**将返回错误。
