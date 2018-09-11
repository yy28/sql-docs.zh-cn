---
title: execute 方法 (java.lang.String，int[]) |Microsoft Docs
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
ms.openlocfilehash: 84d3b4d916b91c95efaff5ad9e995e6bad40a9ad
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "42786603"
---
# <a name="execute-method-javalangstring-int"></a>execute 方法 (java.lang.String, int[])

  运行可返回多项结果的给定的 SQL 语句，并向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 发出信号以指明给定数组中指定的自动生成的键应对检索可用。

## <a name="syntax"></a>语法

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parameters
*sql*

一个**字符串**，其中包含 SQL 语句。

*columnIndexes*

一组 int 数组，指示应该可用的自动生成的键的列索引。

## <a name="return-value"></a>返回值
如果第一个结果为一个结果集，则为“true”。 否则为 **false**。
  
## <a name="exceptions"></a>异常
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
此执行方法是由 java.sql.Statement 接口中的执行方法指定的。

## <a name="see-also"></a>另请参阅

[执行方法&#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement 成员](./sqlserverstatement-members.md)

[SQLServerStatement 类](./sqlserverstatement-class.md)
