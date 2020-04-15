---
title: 更新 - SQL 命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818811c18ed52cef5bdb1c4d97f947bb86e67422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307638"
---
# <a name="update---sql-command"></a>UPDATE - SQL 命令
使用新值更新表中的记录。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅**驱动程序备注**。  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>参数  
 更新 [*数据库名称1！**表名称1*  
 指定使用新值更新记录的表。  
  
 *数据库名称1！* 指定数据库的名称，而不是使用包含表的数据源指定的数据库。 如果数据库不是当前数据库，则必须包含包含该表的数据库的名称。 包括数据库名称后和表名称之前的感叹号 （！） 分隔符。  
  
 设置*Column_Name1*= *eExpression1**，Column_Name2 *Column_Name2*= *eExpression2*  
 指定更新的列及其新值。 如果省略 WHERE 子句，则列中的每一行都会使用相同的值进行更新。  
  
 其中*筛选条件1*[和&#124;或*过滤器条件2*...]  
 指定使用新值更新的记录。  
  
 *筛选器条件*指定记录必须满足的条件才能使用新值进行更新。 您可以根据需要包含尽可能多的筛选条件，将它们与 AND 或 OR 运算符连接。 您还可以使用 NOT 运算符反转逻辑表达式的值，也可以使用**EMPTY**（ ） 检查空字段。  
  
## <a name="remarks"></a>备注  
 更新 - SQL 只能更新单个表中的记录。  
  
 与 REPLACE 不同，UPDATE - SQL 在更新为共享访问的表中的多个记录时使用记录锁定。 这减少了多用户情况下的记录争用，但会降低性能。 为了达到最佳性能，打开表以专供独占使用，或使用**FLOCK**（ ） 锁定表。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当您的应用程序将 ODBC SQL 语句更新发送到数据源时，Visual FoxPro ODBC 驱动程序将该命令转换为 Visual FoxProUPDATE 命令，无需翻译。  
  
## <a name="see-also"></a>另请参阅  
 [删除 - SQL 命令](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
