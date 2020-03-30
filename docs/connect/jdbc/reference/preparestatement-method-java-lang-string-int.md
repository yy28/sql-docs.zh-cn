---
title: prepareStatement 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c91b965498c0b617a02c7707e369a2ba61c0065
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976152"
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement 方法 (java.lang.String)

创建用于将参数化的 SQL 语句发送到数据库的 [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) 对象。

## <a name="syntax"></a>语法

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>parameters
*sql*

包含 SQL 语句的 String  。

## <a name="return-value"></a>返回值
PreparedStatement 对象。

## <a name="exceptions"></a>例外  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>备注
此 prepareStatement 方法是由 java.sql.Connection 接口中的 prepareStatement 方法指定的。

## <a name="see-also"></a>另请参阅

[prepareStatement 方法 &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection 成员](./sqlserverconnection-members.md)

[SQLServerConnection 类](./sqlserverconnection-class.md)
