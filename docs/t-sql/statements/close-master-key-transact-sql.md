---
title: "关闭 MASTER KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE MASTER KEY
- CLOSE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- CLOSE MASTER KEY statement
- database master key [SQL Server], closing
- cryptography [SQL Server], Database Master Key
- closing Database Master Keys
ms.assetid: bb04ef7a-9f3a-437e-a6f9-ba0204082cb9
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e1337667bc7dd03d9943f7b7f76f8a313eeb125
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="close-master-key-transact-sql"></a>CLOSE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  关闭当前数据库的主密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CLOSE MASTER KEY  
```  
  
## <a name="arguments"></a>参数  
 无参数。  
  
## <a name="remarks"></a>注释  
 该语句可反转 OPEN MASTER KEY 执行的操作。 仅当使用 OPEN MASTER KEY 语句在当前会话中打开数据库主密钥时，OSE MASTER KEY 才能成功。  
  
## <a name="permissions"></a>Permissions  
 不需要任何权限。  
  
## <a name="examples"></a>示例  
  
```  
USE AdventureWorks2012;  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO   
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [打开主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


