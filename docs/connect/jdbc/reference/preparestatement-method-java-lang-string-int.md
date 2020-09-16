---
description: prepareStatement 方法 (java.lang.String)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f9cec12d2443e84ef3334e19253a64ff60fea1c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432859"
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement 方法 (java.lang.String)

创建用于将参数化的 SQL 语句发送到数据库的 [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) 对象。

## <a name="syntax"></a>语法

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>参数
*sql*

包含 SQL 语句的 String****。

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
