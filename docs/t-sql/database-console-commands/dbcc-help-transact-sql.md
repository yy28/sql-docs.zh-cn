---
title: "DBCC 帮助 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fd6f0e7ef5c74c3a3f8fc2af9424a2996dfcd98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

返回指定的 DBCC 命令的语法信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 *dbcc_statement* | *@dbcc_statement_var*  
 接收语法信息的 DBCC 命令的名称。 仅提供 DBCC 命令后面的一部分，例如 CHECKDB，而不是 DBCC CHECKDB。  
  
 ?  
 返回可查看其帮助信息的所有 DBCC 命令。  
  
 WITH NO_INFOMSGS  
 取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
DBCC HELP 返回显示指定 DBCC 命令语法的结果集。
  
## <a name="permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色的成员身份。
  
## <a name="examples"></a>示例  
### <a name="a-using-dbcc-help-with-a-variable"></a>A. 使用包含变量的 DBCC HELP  
以下示例返回 DBCC `CHECKDB` 的语法信息。
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>B. 使用包含 ? 选项  
以下示例返回可查看其帮助信息的所有 DBCC 语句。
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

