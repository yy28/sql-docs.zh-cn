---
title: "删除外部库 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 143e9ac0dbe042ebbb034dff847cfc01ea5a5411
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-library-transact-sql"></a>删除外部库 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

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

向数据库添加 ggplot2:

```sql
CREATE EXTERNAL LIBRARY ggplot2 
FROM 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\ggplot2.zip';
```

删除 ggplot2 库。

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

## <a name="see-also"></a>另请参阅  
[创建外部库 (Transact SQL)](create-external-library-transact-sql.md)  
[ALTER 外部库 (Transact SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  


