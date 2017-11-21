---
title: "拖放签名 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81823a549f608bdcddb631084904fb303a1ddc9f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  从存储过程、函数、触发器或程序集中删除数字签名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>参数  
 *模块名*  
 存储过程、函数、程序集或触发器的名称。  
  
 证书*cert_name*  
 用于对存储过程、函数、程序集或触发器进行签名的证书的名称。  
  
 非对称密钥*Asym_key_name*  
 用于对存储过程、函数、程序集或触发器进行签名的非对称密钥的名称。  
  
## <a name="remarks"></a>注释  
 可以在 sys.crypt_properties 目录视图中看到有关签名的信息。  
  
## <a name="permissions"></a>Permissions  
 需要对对象拥有 ALTER 权限，并且对证书或非对称密钥拥有 CONTROL 权限。 如果关联的私钥受密码保护，则用户还必须具有相应的密码。  
  
## <a name="examples"></a>示例  
 以下示例从存储过程 `HumanResourcesDP` 中删除证书 `HumanResources.uspUpdateEmployeeLogin` 的签名。  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.crypt_properties &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [添加签名 &#40;Transact SQL &#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  

