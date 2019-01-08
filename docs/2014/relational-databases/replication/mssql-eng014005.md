---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 418628c33764c6e765e8ba855da20f0890f6191a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800709"
---
# <a name="mssqleng014005"></a>MSSQL_ENG014005
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14005|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法删除发布。 该发布已有订阅。|  
  
## <a name="explanation"></a>解释  
 您试图删除带有关联的订阅的发布。 只有发布不具有相关联的订阅时才可删除它。  
  
## <a name="user-action"></a>用户操作  
 删除发布前请先删除订阅。 如果用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 删除发布，它会提供选项使您可以在删除发布前自动删除所有相关联的订阅。 如果用存储过程，则必须首先显式删除订阅。 有关详细信息，请参阅 [Delete a Push Subscription](delete-a-push-subscription.md) 和 [Delete a Pull Subscription](delete-a-pull-subscription.md)。  
  
 如果看起来发布不存在订阅或者在创建发布时看到此错误，则说明可能存在以前删除时未完全清除的订阅。 对数据库执行 [sp_removedbreplication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)，以删除所有与复制相关的对象和设置。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
