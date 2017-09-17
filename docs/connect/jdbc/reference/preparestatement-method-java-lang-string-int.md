---
title: "prepareStatement 方法 (java.lang.String) |Microsoft 文档"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2452837aba5b8c5a146c12de838a3259f65be38
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement 方法 (java.lang.String)

创建[SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md)发送的对象参数化到数据库的 SQL 语句。

## <a name="syntax"></a>语法

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parameters
*sql*

A**字符串**包含 SQL 语句。

## <a name="return-value"></a>返回值
一个 PreparedStatement 对象。

## <a name="exceptions"></a>异常  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>注释
由 java.sql.Connection 接口中的 prepareStatement 方法指定此 prepareStatement 方法。

## <a name="see-also"></a>另请参阅

[prepareStatement 方法 &#40;SQLServerConnection &#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection 成员](./sqlserverconnection-members.md)

[SQLServerConnection 类](./sqlserverconnection-class.md)

