---
title: CERT_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- CERT_ID
- CERT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3abed6a762708581344c189ecf4ef6c0fd5331d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="certid-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回证书的 ID。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>参数  
**'** *cert_name* **'**  
数据库中证书的名称。
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="remarks"></a>Remarks  
证书名称可以在 [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 目录视图中看到。
  
## <a name="permissions"></a>权限  
需要对证书具有某些权限，并且未拒绝向调用方授予该证书的 VIEW DEFINITION 权限。
  
## <a name="examples"></a>示例  
以下示例返回名为 `ABerglundCert3` 的证书的 ID。
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[sys.certificates (Transact-SQL)](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)  
[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
