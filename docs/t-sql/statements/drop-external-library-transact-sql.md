---
title: "删除外部库 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: c157270e83ccfd3277356863b26c49222691e9e3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="drop-external-library-transact-sql"></a>删除外部库 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

删除现有的包库。

## <a name="syntax"></a>语法  

```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>参数

**library_name**

指定现有的包库的名称。

库的应用范围限定为用户。 也就是说，库名称被视为在特定用户或所有者的上下文中是唯一。

**owner_name**

指定用户或角色拥有外部库的名称。

数据库所有者可以删除由其他用户创建的库。

### <a name="return-values"></a>返回值

如果该语句已成功，则返回一条信息性消息。

## <a name="remarks"></a>注释

与其他不同`DROP`SQL Server 中的语句，此语句支持指定可选 authorization 子句。 这允许**dbo**或中的用户**db_owner**角色删除包库上载常规用户数据库中。

## <a name="examples"></a>示例

添加自定义的 R 包，名为`customPackage`，到数据库：

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

删除`customPackage`库。

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>另请参阅  
[创建外部库 (Transact SQL)](create-external-library-transact-sql.md)  
[ALTER 外部库 (Transact SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

