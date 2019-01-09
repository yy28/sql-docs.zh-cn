---
title: 设置断点 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- Set Breakpoints dialog box
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0c2c543343bd602be75d600a489edfd84663790b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776097"
---
# <a name="set-breakpoints"></a>“设置断点”
  可以使用 **“设置断点”** 对话框，指定要启用断点和控制断点行为的事件。  
  
## <a name="options"></a>选项  
 **已启用**  
 选择此选项可以对事件启用断点。  
  
 **中断条件**  
 查看可设置断点的事件列表。  
  
 **命中计数类型**  
 指定断点生效的时间。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**始终**|断点命中时始终挂起执行。|  
|**命中计数等于**|断点发生的次数等于命中计数时挂起执行。|  
|**命中计数大于或等于**|断点发生的次数等于或大于命中计数时挂起执行。|  
|**命中计数倍增基数**|断点发生的次数为命中计数的倍数时挂起执行。 例如，如果将此选项设置为 5，则每命中五次就挂起执行。|  
  
 **命中计数**  
 指定触发中断的命中次数。 如果断点始终有效，则此选项将不可用。  
  
## <a name="see-also"></a>请参阅  
 [调试控制流](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
