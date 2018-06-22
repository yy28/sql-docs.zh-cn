---
title: 设置断点 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- Set Breakpoints dialog box
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: acef1e3e3cc297a54471ed124bfa5984b2980d9a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016555"
---
# <a name="set-breakpoints"></a>“设置断点”
  可以使用 **“设置断点”** 对话框，指定要启用断点和控制断点行为的事件。  
  
## <a name="options"></a>“常规”  
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
  
  