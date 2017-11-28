---
title: "关闭对称密钥 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE SYMMETRIC KEY
- CLOSE_SYMMETRIC_KEY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- closing symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], closing
- CLOSE SYMMETRIC KEY statement
- cryptography [SQL Server], symmetric keys
ms.assetid: 3b083cbb-3c6a-4f59-8d34-601db1efcc83
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2e65502932c646f539e923fe905854234534eac
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="close-symmetric-key-transact-sql"></a>CLOSE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  关闭对称密钥，或关闭在当前会话中打开的所有对称密钥。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CLOSE { SYMMETRIC KEY key_name | ALL SYMMETRIC KEYS }  
```  
  
## <a name="arguments"></a>参数  
 *Key_name*  
 要关闭的对称密钥的名称。  
  
## <a name="remarks"></a>注释  
 打开的对称密钥将绑定到会话而不是安全上下文。 打开的密钥将持续有效，直到它显式关闭或会话终止。 关闭所有对称密钥将关闭通过当前会话中打开任何数据库主密钥[OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md)语句。  有关打开密钥的信息会显示在[sys.openkeys &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md)目录视图。  
  
## <a name="permissions"></a>Permissions  
 关闭对称密钥不需要显式权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-closing-a-symmetric-key"></a>A. 关闭对称密钥  
 以下示例关闭对称密钥 `ShippingSymKey04`。  
  
```  
CLOSE SYMMETRIC KEY ShippingSymKey04;  
GO  
```  
  
### <a name="b-closing-all-symmetric-keys"></a>B. 关闭所有对称密钥  
 以下示例关闭在当前会话中打开的所有对称密钥，还将关闭显式打开的数据库主密钥。  
  
```  
CLOSE ALL SYMMETRIC KEYS;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [删除对称密钥 &#40;Transact SQL &#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)  
  
  
