---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 25d4c4acf67de7443d9dfab68e67fe0750ff0a37
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62762668"
---
# <a name="mssqlserver_9002"></a>MSSQLSERVER_9002
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9002|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_IS_FULL|  
|消息正文|数据库 '%.*ls' 的事务日志已满。 若要查明无法重用日志中的空间的原因，请参阅 sys.databases 中的 log_reuse_wait_desc 列。|  
  
## <a name="explanation"></a>说明  
 数据库日志空间不足。 **sys.databases** 中的 **log_reuse_wait_desc** 列说明无法重用日志中的空间的原因。  
  
## <a name="user-action"></a>用户操作  
 使用 **sys.databases** 确定日志已满的原因，然后更正该情况。 有关详细信息，请参阅 Server SQL 联机丛书中的“解决事务日志已满的问题（错误 9002）”。  
  
## <a name="see-also"></a>另请参阅  
 [排查事务日志 &#40;SQL Server 错误 9002&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
