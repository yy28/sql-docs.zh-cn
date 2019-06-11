---
title: sys.sql_feature_restrictions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_sql_feature_restrictions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_feature_restrictions catalog view
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b583afef9f52da7801384d4a7a9c76deaf8d4ee4
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822674"
---
# <a name="syssqlfeaturerestrictions-transact-sql"></a>sys.sql_feature_restrictions (Transact SQL)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

返回数据库中的每个限制的一行。
  
| 列名 | 数据类型 | Description |
|-------------|-----------|-------------|
| class       | nvarchar(128) | 此限制适用的对象的类 |
| 对象 (object)      | nvarchar(256) | 此限制适用的对象的名称 |
| 功能     | nvarchar(128) | 是受限制的功能 |
  
## <a name="remarks"></a>备注

当前可以是受限制的以下功能：

| 功能          | Description |
|------------------|-------------|
| N'ErrorMessages' | 限制时，将屏蔽的错误消息中的任何用户数据。 |
| N'Waitfor       | 限制时，该命令将立即返回不使用任何延迟。 |
  
## <a name="permissions"></a>权限

正在执行的主体必须具有`CONTROL`针对数据库的权限。
  
## <a name="see-also"></a>请参阅

 [功能限制](../../relational-databases/security/feature-restrictions.md)
