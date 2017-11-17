---
title: "事务隔离级别 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0acd70fad20d0ad1c2727f93da52b2e938ee21fd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="transaction-isolation-levels"></a>事务隔离级别
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保证通过目录视图、兼容性视图、信息架构视图、元数据发出内置函数访问元数据的查询遵守锁提示。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]在内部仅按照 READ COMMITTED 隔离级别进行元数据访问。 如果事务有一个隔离级别（例如 SERIALIZABLE），并且您尝试在事务中使用目录视图或元数据发出内置函数访问元数据，则查询将一直运行，直到它们按照 READ COMMITTED 隔离级别完成。 但是，在快照隔离级别下，访问元数据可能会因并发的 DDL 操作而失败。 这是因为未将元数据版本化。 因此，在快照隔离级别下访问下列内容可能会失败：  
  
-   目录视图  
  
-   兼容性视图  
  
-   信息架构视图  
  
-   元数据发出内置函数  
  
-   **sp_help**组的存储过程  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端目录过程  
  
-   动态管理视图和函数  
  
 有关隔离级别的详细信息，请参阅[SET TRANSACTION ISOLATION LEVEL &#40;Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 下表概述了各种隔离级别下的元数据访问。  
  
|隔离级别|是否支持|遵守|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|是|不保证|  
|READ COMMITTED|是|是|  
|REPEATABLE READ|是|是|  
|SNAPSHOT ISOLATION|是|是|  
|SERIALIZABLE|是|是|  
  
  

