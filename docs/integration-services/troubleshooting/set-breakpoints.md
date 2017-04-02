---
title: "设置断点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.setbreakpoints.f1"
helpviewer_keywords: 
  - "“设置断点”对话框"
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# 设置断点
  可以使用 **“设置断点”** 对话框，指定要启用断点和控制断点行为的事件。  
  
## 选项  
 **已启用**  
 选择此选项可以对事件启用断点。  
  
 **中断条件**  
 查看可设置断点的事件列表。  
  
 **命中计数类型**  
 指定断点生效的时间。  
  
|“值”|Description|  
|-----------|-----------------|  
|**始终**|断点命中时始终挂起执行。|  
|**命中计数等于**|断点发生的次数等于命中计数时挂起执行。|  
|**命中计数大于或等于**|断点发生的次数等于或大于命中计数时挂起执行。|  
|**命中计数倍增基数**|断点发生的次数为命中计数的倍数时挂起执行。 例如，如果将此选项设置为 5，则每命中五次就挂起执行。|  
  
 **命中计数**  
 指定触发中断的命中次数。 如果断点始终有效，则此选项将不可用。  
  
## 另请参阅  
 [调试控制流](../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  