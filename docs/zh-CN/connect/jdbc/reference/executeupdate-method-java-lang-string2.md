---
title: executeUpdate 方法 (java.lang.String) |Microsoft 文档
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb1b5e42d05508ea83b37985356c4eb0da6c68d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-javalangstring"></a>executeUpdate 方法 (java.lang.String)

运行给定的 SQL 语句，可以是 INSERT、UPDATE、MERGE 或 DELETE 语句；或不返回任何内容的 SQL 语句，例如 SQL DDL 语句。

## <a name="syntax"></a>语法

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parameters
*sql*

A**字符串**包含 SQL 语句。

## <a name="return-value"></a>返回值
**Int** ，该值指示行受影响，则为 0 的数，如果使用的 DDL 语句。

## <a name="exceptions"></a>异常
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>注释
由 java.sql.PreparedStatement 接口中的 executeUpdate 方法指定此 executeUpdate 方法。

由于在创建对象时指定 SQLServerPreparedStatement 对象的 SQL 语句，则将调用此方法将导致异常。

## <a name="see-also"></a>另请参阅

[executeUpdate 方法&#40;SQLServerPreparedStatement&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[SQLServerPreparedStatement 成员](./sqlserverpreparedstatement-members.md)

[SQLServerPreparedStatement 类](./sqlserverpreparedstatement-class.md)
