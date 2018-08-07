---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: HeidiSteen
ms.author: heidist
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f17e31aca14d38a6d8c124ce28f2936c1b28957c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453031"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

删除现有包库。 包库供受支持的外部运行时（R 或 Python）使用。

## <a name="syntax"></a>语法

```sql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>参数

**library_name**

指定现有包库的名称。

库的应用范围限定为用户。 在特定用户或所有者的上下文中，库名称必须是唯一的。

**owner_name**

指定拥有外部库的用户或角色的名称。

数据库所有者可以删除由其他用户创建的库。

## <a name="permissions"></a>Permissions

必须拥有 ALTER ANY EXTERNAL LIBRARY 权限，才能删除库。 默认情况下，任何数据库所有者或对象所有者也可以删除外部库。

### <a name="return-values"></a>返回值

如果语句成功，则返回信息性消息。

## <a name="remarks"></a>Remarks

不同于 SQL Server 中的其他 `DROP` 语句，此语句支持指定一个可选的授权子句。 这允许 db_owner 角色中的 dbo 或用户删除由数据库的常规用户上传的包库。

## <a name="examples"></a>示例

将自定义 R 包 `customPackage` 添加到数据库：

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```

删除 `customPackage` 库。

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>另请参阅

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

