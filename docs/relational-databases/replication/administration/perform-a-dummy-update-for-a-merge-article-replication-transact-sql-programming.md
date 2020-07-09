---
title: 虚拟合并项目更新（复制 SP）
description: 使用 Transact-SQL 复制存储过程对合并复制中使用的合并项目执行虚拟更新。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 182e8bbe99c16de1415464988eda0d8966806e3b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901709"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>执行合并项目的虚更新（复制 Transact-SQL 编程）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  合并复制将触发器作为复制过程的一部分；在对发布的表进行更新时，将会触发更新触发器。 在某些情况下，无需触发触发器便可以更新数据，比如在 WRITETEXT 和 UPDATETEXT 操作期间。 在这些情况下，您需要显式添加虚 UPDATE 语句来复制更改。 可以使用复制存储过程添加虚 UPDATE 语句。  
  
### <a name="to-add-a-dummy-update-statement"></a>添加虚 UPDATE 语句  
  
1.  请对需要虚更新的合并发布表中的行执行操作（例如，UPDATETEXT）。  
  
2.  在服务器（发布服务器或订阅服务器）的进行了更改的数据库中，执行 [sp_mergedummyupdate (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md)。 为 `@source_object` 指定进行了更改的表，并为 `@rowguid` 指定发生了更改的行的唯一标识符。  
  
3.  同步此订阅以复制更改行。  
  
  
