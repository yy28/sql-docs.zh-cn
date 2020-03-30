---
title: CERT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 10f97749970337435b14ff0d1dc14df42ad48daf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68040131"
---
# <a name="cert_id-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函数返回证书的 ID 值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>参数  
**'** *cert_name* **'**  

数据库中证书的名称。
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="remarks"></a>备注  
[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 目录视图中显示证书名称。
  
## <a name="permissions"></a>权限  
需要对证书具有相应的权限，并且调用方对证书的 VIEW DEFINITION 权限没有被拒绝。 有关证书权限的详细信息，请参阅 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md#permissions)。
  
## <a name="examples"></a>示例  
此示例返回名为 `ABerglundCert3` 的证书的 ID。
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[sys.certificates (Transact-SQL)](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)  
[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
