---
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3b465c4e4c7a7484413f93aa2bb547e9685297bd
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8525"></a>MSSQLSERVER_8525
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8525|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|分布式事务已完成。 请将此会话登记到新事务或 NULL 事务中。|  
  
## <a name="explanation"></a>解释  
将分布式事务处理协调器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配合使用的编程模型需要应用程序显式登记到分布式事务并从中脱离出来。  
  
满足以下四个条件时会出现此错误：  
  
-   应用程序已登记到分布式事务中。  
  
-   无论原因如何，该事务已结束（已提交或回滚）。  
  
-   用户应用程序并未显式地从分布式事务中脱离或显式地登记到新的分布式事务中。  
  
-   应用程序尝试执行任何脱离现有分布式事务或登记到新的分布式事务以外的事务操作，如发出查询或启动本地事务。  
  
错误状态 1 在应用程序执行创建本地事务的操作时使用，状态 2 在应用程序尝试登记到绑定会话时使用。  
  
## <a name="user-action"></a>用户操作  
应用程序登记到分布式事务中之后，应用程序必须显式地从分布式事务中脱离或登记到另一个分布式事务中。 这样将从上一个登记的事务中隐式脱离。 有关从分布式事务脱离或登记到其中的准确语法，请参见该应用程序的编程接口手册。  
  

