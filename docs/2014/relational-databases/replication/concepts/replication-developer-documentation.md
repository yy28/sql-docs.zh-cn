---
title: 开发人员&#39;s 指南 （复制） |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- replication
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
caps.latest.revision: 39
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fb0ffaba9b07a24c6d3ae27e442c4b4e41d8f255
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018616"
---
# <a name="developer39s-guide-replication"></a>开发人员&#39;s 指南 （复制）
  如果能够以编程方式配置、维护和监视复制拓扑，则不仅可以简化重复性的复制任务，而且还可以改善基于复制的应用程序的用户体验。 通过复制编程，最终用户可以获得自定义的复制功能，既无须熟悉复制存储过程和复制代理可执行文件，也无须使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 实现的复制用户界面。  
  
 在下面的应用场景中，您的应用程序可从对复制服务的编程访问中获益：  
  
-   向现有最终用户应用程序添加复制功能，如当用户单击按钮时同步请求订阅。  
  
-   为远程管理复制创建基于 Web 的用户接口。  
  
-   创建仅公开部分管理功能的自定义用户接口，可用于从单个位置远程管理多个复制拓扑，或组合管理功能与同步功能。  
  
-   通过添加对发布、订阅的状态或对分发服务器执行监视的功能来改进现有监视工具。  
  
-   创建自定义应用程序，以管理订阅或与 Oracle 发布服务器同步订阅。  
  
-   编写同步合并订阅时执行的自定义业务规则。  
  
-   生成可在配置新订阅服务器时重复运行的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不但允许您以编程方式控制复制代理，还使您能够以编程方式管理和监视复制拓扑。 若要了解有关复制编程的详细信息，请参阅[复制编程概念](replication-programming-concepts.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [复制编程概念](replication-programming-concepts.md)  
 介绍开发使用复制的应用程序的计划步骤。  
  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)  
 介绍如何在复制拓扑中使用系统存储过程来提供编程访问。  
  
 [复制管理对象概念](replication-management-objects-concepts.md)  
 解释使用复制管理对象 (RMO) 的相关概念。 复制管理对象是一个封装了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的复制功能的托管代码程序集。  
  
 [复制代理可执行文件概念](replication-agent-executables-concepts.md)  
 介绍如何使用复制代理可执行文件。  
  
 [开发人员指南：操作指南主题（复制）](../developer-s-guide-how-to-topics-replication.md)  
 提供与复制相关的操作指南主题的列表。  
  
  