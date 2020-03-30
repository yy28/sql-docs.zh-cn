---
title: execute 方法 (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e96e0c9c957522db6a766b3491d394b7337d7b6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954985"
---
# <a name="execute-method-javalangstring-int"></a>execute 方法 (java.lang.String, int[])

  运行可返回多项结果的给定的 SQL 语句，并向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 发出信号以指明给定数组中指定的自动生成的键应对检索可用。

## <a name="syntax"></a>语法

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>parameters
*sql*

包含 SQL 语句的 String  。

columnIndexes 

一组 int 数组，指示应该可用的自动生成的键的列索引  。

## <a name="return-value"></a>返回值
如果第一个结果为一个结果集，则为“true”  。 否则为 **false**。
  
## <a name="exceptions"></a>例外
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>备注
此执行方法是由 java.sql.Statement 接口中的执行方法指定的。

## <a name="see-also"></a>另请参阅

[execute 方法 (SQLServerStatement)](./execute-method-sqlserverstatement.md)

[SQLServerStatement 成员](./sqlserverstatement-members.md)

[SQLServerStatement 类](./sqlserverstatement-class.md)
