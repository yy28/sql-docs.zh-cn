---
title: 执行方法 (java.lang.String、 int[]) |Microsoft 文档
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afe080df57157ae62e604ff8057027a45df39fc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833322"
---
# <a name="execute-method-javalangstring-int"></a>execute 方法 (java.lang.String, int[])

  运行给定的 SQL 语句可以返回多个结果，以及信号[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion-md.md)]指示给定的数组中的自动生成密钥应该进行检索。

## <a name="syntax"></a>语法

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parameters
*sql*

A**字符串**包含 SQL 语句。

*columnIndexes*

数组**int**s，该值指示应将提供的自动生成的键的列索引。

## <a name="return-value"></a>返回值
**true**如果第一个结果是一个结果集。 否则为 **false**。
  
## <a name="exceptions"></a>异常
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>注释
由 java.sql.Statement 接口中的 execute 方法指定此 execute 方法。

## <a name="see-also"></a>另请参阅

[执行方法&#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement 成员](./sqlserverstatement-members.md)

[SQLServerStatement 类](./sqlserverstatement-class.md)
