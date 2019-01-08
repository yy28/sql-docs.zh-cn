---
title: sys.sp_flush_log (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fba195d53911264716c73b54ea8c639ca37951e6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418308"
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  将当前数据库的事务日志刷新至磁盘，从而强化所有之前已提交的延迟持久事务。  
  
 如果您出于性能优势原因而选择使用延迟事务持续性，但还想对在服务器崩溃或故障转移时丢失的数据量进行有保证的限制，请定期执行 `sys.sp_flush_log`。 例如，如果你想要确保不丢失多于 x 秒的数据，将执行`sp_flush_log`每隔 x 秒。  
  
 执行 `sys.sp_flush_log` 可保证所有之前提交的延迟持久事务都是持久的。 请参阅概念性主题[控制事务持续性](../../relational-databases/logs/control-transaction-durability.md)有关详细信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parameters  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 返回代码 1 表示成功。  任何其他值表示失败。  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="sample-code"></a>示例代码  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
