---
title: UPDATE-SQL 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbd5ec98791d782fe7ad1fdb1e1884b646dcf9f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818305"
---
# <a name="update---sql-command"></a>UPDATE - SQL 命令
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
  
 *DatabaseName1 ！* 指定包含表的数据源与指定的数据库的数据库的名称。 必须包括包含表，如果数据库不是当前的数据库的名称。 包含感叹号 （！） 分隔符之后的数据库名称和表名称之前。  
  
 设置*Column_Name1*= *eExpression1*[， *Column_Name2*= *eExpression2*  
 指定更新的列及其新值。 如果省略 WHERE 子句，具有相同值更新列中的每个行。  
  
 其中*FilterCondition1*[AND&#124;或者*FilterCondition2*...]  
 指定使用新值更新的记录。  
  
 *FilterCondition*指定记录使用新值更新而必须满足的条件。 可以包含任意数量的筛选条件根据需要，将它们连接用 AND 或 OR 运算符。 此外可以使用 NOT 运算符来反转逻辑表达式的值也可以使用**空**（) 以检查是否有一个空的字段。  
  
## <a name="remarks"></a>备注  
 更新-SQL 可以更新仅在单个表中的记录。  
  
 与替换，不同更新-SQL 使用记录锁定时正在更新表中的多个记录可供使用共享访问。 这会降低在多用户的情况下记录争用，但可能会降低性能。 获得最佳性能，打开表的独占使用，或者使用**纷纷采用**（) 以锁定表。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将发送到数据源的 ODBC SQL 语句更新时，Visual FoxPro ODBC 驱动程序将不转换 Visual FoxProUPDATE 命令转换为命令。  
  
## <a name="see-also"></a>请参阅  
 [DELETE-SQL 命令](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
