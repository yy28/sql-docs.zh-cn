---
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0e254e38eabc62ab3e11e7d8ab1a3396c465470
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913232"
---
# <a name="mssqlserver_8525"></a>MSSQLSERVER_8525
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8525|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|分布式事务已完成。 请将此会话登记到新事务或 NULL 事务中。|  
  
## <a name="explanation"></a>说明  
 将分布式事务处理协调器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配合使用的编程模型需要应用程序显式登记到分布式事务并从中脱离出来。  
  
 满足以下四个条件时会出现此错误：  
  
-   应用程序已登记到分布式事务中。  
  
-   无论原因如何，该事务已结束（已提交或回滚）。  
  
-   用户应用程序并未显式地从分布式事务中脱离或显式地登记到新的分布式事务中。  
  
-   应用程序尝试执行任何脱离现有分布式事务或登记到新的分布式事务以外的事务操作，如发出查询或启动本地事务。  
  
 错误状态 1 在应用程序执行创建本地事务的操作时使用，状态 2 在应用程序尝试登记到绑定会话时使用。  
  
## <a name="user-action"></a>用户操作  
 应用程序登记到分布式事务中之后，应用程序必须显式地从分布式事务中脱离或登记到另一个分布式事务中。 这样将从上一个登记的事务中隐式脱离。 有关从分布式事务脱离或登记到其中的准确语法，请参见该应用程序的编程接口手册。  
  
  
