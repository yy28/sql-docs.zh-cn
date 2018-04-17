---
title: 更新-SQL 命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8c1189955ee62fd14484816358feffc38e002c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="update---sql-command"></a>更新-SQL 命令
使用新值更新表中的记录。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅**驱动程序备注**。  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>参数  
 更新 [ *DatabaseName1 ！*]*TableName1*  
 指定使用新值更新记录的表。  
  
 *DatabaseName1 ！* 指定包含表的数据源与指定的数据库之外的数据库的名称。 必须包括包含表，如果数据库不是当前的数据库的名称。 之后的数据库名称和表名称之前，请包括感叹号 （！） 分隔符。  
  
 设置*Column_Name1*= *eExpression1*[， *Column_Name2*= *eExpression2*  
 指定更新的列和其新值。 如果省略 WHERE 子句，使用相同的值更新列中的每个行。  
  
 其中*FilterCondition1*[AND&#124;或者*FilterCondition2*...]  
 指定使用新值更新的记录。  
  
 *FilterCondition*指定记录为使用新值更新而必须满足的条件。 可以包含任意数量的筛选条件根据需要，将它们连接使用 AND 或 OR 运算符。 你还可以使用 NOT 运算符颠倒的逻辑表达式时，值或可以使用**空**（) 检查是否有一个空的字段。  
  
## <a name="remarks"></a>注释  
 更新-SQL 可以更新仅在单个表的记录。  
  
 与替换，不同更新-SQL 使用记录锁定更新表中的多个记录打开以进行共享访问时。 这将减少在多用户情况下记录争用，但可能会降低性能。 为获得最佳性能，打开该表的独占使用，或者使用**FLOCK**（) 锁定表。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将 ODBC SQL 语句更新发送到数据源时，Visual FoxPro ODBC 驱动程序将不转换 Visual FoxProUPDATE 命令转换为命令。  
  
## <a name="see-also"></a>另请参阅  
 [删除的 SQL 命令](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
