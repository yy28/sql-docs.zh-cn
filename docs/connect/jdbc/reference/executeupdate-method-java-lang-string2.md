---
title: executeUpdate 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04b3bdcd2b495513500d07583fadc910fe9c13a9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954684"
---
# <a name="executeupdate-method-javalangstring"></a>executeUpdate 方法 (java.lang.String)

运行给定的 SQL 语句，可以是 INSERT、UPDATE、MERGE 或 DELETE 语句；或不返回任何内容的 SQL 语句，例如 SQL DDL 语句。

## <a name="syntax"></a>语法

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>parameters
*sql*

包含 SQL 语句的 String  。

## <a name="return-value"></a>返回值
一个指示受影响的行数的 int，如果使用 DDL 语句，则为 0  。

## <a name="exceptions"></a>例外
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>备注
此 executeUpdate 方法是由 java.sql.PreparedStatement 接口中的 executeUpdate 方法指定的。

调用此方法将导致异常，因为在创建 SQLServerPreparedStatement 对象时指定了该对象的 SQL 语句。

## <a name="see-also"></a>另请参阅

[executeUpdate 方法 &#40;SQLServerPreparedStatement&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[SQLServerPreparedStatement 成员](./sqlserverpreparedstatement-members.md)

[SQLServerPreparedStatement 类](./sqlserverpreparedstatement-class.md)
