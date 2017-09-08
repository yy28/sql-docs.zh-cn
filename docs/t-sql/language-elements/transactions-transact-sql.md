---
title: "事务 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8660d0ac8d6205a94fdab24f41e41bac40a8671e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="transactions-transact-sql"></a>事务 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  事务是单个工作单元。 如果某一事务成功，则在该事务中进行的所有数据修改均会提交，成为数据库中的永久组成部分。 如果事务遇到错误且必须取消或回滚，则所有数据修改均被清除。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以下列事务模式运行。  
  
 自动提交事务  
 每条单独的语句都是一个事务。  
  
 显式事务  
 每个事务均以 BEGIN TRANSACTION 语句显式开始，以 COMMIT 或 ROLLBACK 语句显式结束。  
  
 隐式事务  
 在前一个事务完成时新事务隐式启动，但每个事务仍以 COMMIT 或 ROLLBACK 语句显式完成。  
  
 批处理级事务  
 只能应用于多个活动结果集 (MARS)，在 MARS 会话中启动的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 显式或隐式事务变为批处理级事务。 当批处理完成时没有提交或回滚的批处理级事务自动由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进行回滚。  
  
## <a name="in-this-section"></a>本节内容  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供以下事务语句。  
  
|||  
|-|-|  
|[开始分布式事务](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[开始事务](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[回滚工作](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[提交事务](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[保存事务](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[提交工作](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>另请参阅  
 [设置 IMPLICIT_TRANSACTIONS &#40;Transact SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)  
  
  
