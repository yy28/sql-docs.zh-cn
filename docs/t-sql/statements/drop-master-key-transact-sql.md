---
title: "删除 MASTER KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP MASTER KEY
- DROP_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing Database Master Keys
- database master key [SQL Server], removing
- encryption [SQL Server], Database Master Key
- DROP MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- dropping Database Master Keys
- deleting Database Master Keys
ms.assetid: 5ccef797-408f-4964-80da-965d8e1ccba7
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf519ae4d69429338522a98805616352f3c57cf5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-master-key-transact-sql"></a>DROP MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  从当前数据库中删除主密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP MASTER KEY  
```  
  
## <a name="arguments"></a>参数  
 该语句不带任何参数。  
  
## <a name="remarks"></a>注释  
 如果数据库中的任何私钥都受主密钥保护，则删除操作将会失败。  
  
## <a name="permissions"></a>Permissions  
 要求对数据库具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例删除 `AdventureWorks2012` 数据库的主密钥。  
  
```  
USE AdventureWorks2012;  
DROP MASTER KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例删除主密钥。  
  
```  
USE master;  
DROP MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [打开主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [关闭 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [备份主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [还原 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


