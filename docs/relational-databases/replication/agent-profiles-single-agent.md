---
title: "代理配置文件（单个代理） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.profiles.perfprofileagentname.f1"
helpviewer_keywords: 
  - "“代理配置文件”对话框"
ms.assetid: 22713555-c496-4ce1-8ec7-4ae75cfadca8
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 代理配置文件（单个代理）
  可以使用 **“代理配置文件”** 对话框管理代理的配置文件。 代理配置文件为每个代理提供了一种便于管理运行时参数的方法。 每个代理均有一个默认配置文件，某些代理还有附加的预定义配置文件。 例如，合并代理有一个为低带宽连接设计的“慢速链接”配置文件。 预定义配置文件对于大多数应用程序已经足够，不过，您仍然可以创建用户定义的配置文件，以便自定义代理行为。  
  
## 选项  
 **作为新项的默认值**  
 选择在为给定类型的代理创建作业时将使用的配置文件。 例如，如果创建指向合并发布的多个订阅，则每个订阅的合并代理作业都将使用选定的配置文件。 如果希望更改现有作业的配置文件，请选择一个配置文件，再单击 **“更改现有代理”**。  
  
 **名称**  
 配置文件的名称。  
  
 **类型**  
 配置文件的类型︰ **用户** （用户定义的） 或 **系统** （预定义）。  
  
 **属性(...)**  
 单击此项可查看用于代理配置文件中每个参数的值。  
  
 **新建**  
 单击此项可创建一个新的配置文件。  
  
 **删除**  
 选择用户定义的配置文件，然后单击 **删除** 若要删除该配置文件。 不能删除预定义的配置文件。  
  
 **更改现有代理**  
 选择一个配置文件，然后单击 **更改现有代理** 指定的代理的给定类型的所有现有作业应使用所选配置文件。 例如，如果创建了指向合并发布的多个订阅，并且希望更改配置文件以指定其中每个订阅的合并代理作业都应使用 **“慢速链接代理配置文件”**，请选择该配置文件，再单击 **“更改现有代理”**。  
  
## 另请参阅  
 [处理复制代理配置文件](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  