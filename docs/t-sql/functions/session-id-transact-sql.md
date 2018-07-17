---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2f29f5ba188f70313f94ac4b05f03c7fe8a0575a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783228"
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  返回当前 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 会话的 ID。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>返回值  
 返回 nvarchar(32) 值。  
  
## <a name="general-remarks"></a>一般备注  
 会话 ID 在连接建立时分配给每个用户连接。 它在连接期间都存在。 连接结束时，会话 ID 也会解除。  
  
 会话 ID 以字母字符“SID”开头。 这些字母字符区分大小写，在 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 命令中使用会话 ID 时必须大写。  
  
 可以查询视图 [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 以检索与此函数相同的信息。  
  
## <a name="examples"></a>示例  
 以下示例返回当前会话 ID。  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>另请参阅  
 [DB_NAME (Transact-SQL)](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION（SQL 数据仓库）](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
