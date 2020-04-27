---
title: 执行合并项目的虚更新（复制 Transact-sql 编程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 691988cd229f9b0c9ab81f31713a2b2e46806bdb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63162006"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>执行合并项目的虚更新（复制 Transact-SQL 编程）
  合并复制将触发器作为复制过程的一部分；在对发布的表进行更新时，将会触发更新触发器。 在某些情况下，无需触发触发器便可以更新数据，比如在 WRITETEXT 和 UPDATETEXT 操作期间。 在这些情况下，您需要显式添加虚 UPDATE 语句来复制更改。 可以使用复制存储过程添加虚 UPDATE 语句。  
  
### <a name="to-add-a-dummy-update-statement"></a>添加虚 UPDATE 语句  
  
1.  请对需要虚更新的合并发布表中的行执行操作（例如，UPDATETEXT）。  
  
2.  在服务器（发布服务器或订阅服务器）的进行了更改的数据库中，执行 [sp_mergedummyupdate (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql)。 指定对其进行更改的表**@source_object**，并指定的已更改行的唯一标识符。 **@rowguid**  
  
3.  同步此订阅以复制更改行。  
  
  
