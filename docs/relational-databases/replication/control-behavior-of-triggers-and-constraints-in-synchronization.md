---
title: 同步过程中触发器和约束的控制行为
description: 了解如何在 SQL Server 复制发布的同步过程中防止执行触发器或强制执行约束。
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2b0e768712d1987755f100f4db555a5e09f6db7c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "76284697"
---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>同步中触发器和约束的控制行为
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  在同步期间，复制代理对复制表执行 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)、[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 和 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 语句，这可能导致执行这些表上的数据操作语言 (DML) 触发器。 有些情况下，可能需要在同步期间防止这些触发器触发或防止约束被强制执行。 此行为取决于触发器或约束的创建方式。  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>防止触发器在同步期间执行  
  
1.  创建新触发器时，请指定 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md) 的 NOT FOR REPLICATION 选项。  
  
2.  对于现有触发器，请指定 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md) 的 NOT FOR REPLICATION 选项。  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>防止约束在同步期间被强制执行  
  
1.  创建新 CHECK 或 FOREIGN KEY 约束时，请在 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 的约束定义中指定 CHECK NOT FOR REPLICATION 选项。  
  
## <a name="see-also"></a>另请参阅  
 [创建表（数据库引擎）](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
