---
title: "KEY_GUID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Key_GUID_TSQL
- Key_GUID
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 723186a0489186baa1afeda87d53a71c4d303423
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="keyguid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回数据库中对称密钥的 GUID。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
## <a name="arguments"></a>参数  
  *Key_Name*   
 数据库中对称密钥的名称。  
  
## <a name="return-types"></a>返回类型  
 **uniqueidentifier**  
  
## <a name="remarks"></a>注释  
 如果创建密钥时指定了标识值，则其 GUID 为该标识值的 MD5 哈希。 如果未指定标识值，则服务器生成 GUID。  
  
 如果密钥为临时密钥，则密钥名称必须以数字符号 (#) 开头。  
  
## <a name="permissions"></a>Permissions  
 因为临时密钥只适用于创建它们的会话，所以访问它们不需要任何权限。 若要访问非临时密钥，调用者需要对该密钥具有相应权限，并且必须具有该密钥的 VIEW 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回称为 `ABerglundKey1` 的对称密钥的 GUID。  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  
