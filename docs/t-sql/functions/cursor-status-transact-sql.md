---
title: "CURSOR_STATUS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURSOR_STATUS
- CURSOR_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], cursors
- CURSOR_STATUS function
- cursors [SQL Server], status information
ms.assetid: 3a4a840e-04f8-43bd-aada-35d78c3cb6b0
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e88dd4f14d8bd6fc90c40df101bfd9b2895bf229
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

一个标量函数，它允许存储过程的调用方确定该存储过程是否已为给定的参数返回了游标和结果集。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CURSOR_STATUS   
     (  
          { 'local' , 'cursor_name' }   
          | { 'global' , 'cursor_name' }   
          | { 'variable' , 'cursor_variable' }   
     )  
```  
  
## <a name="arguments"></a>参数  
'local'  
指定一个常量，该常量指示游标的源是一个本地游标名。
  
*cursor_name*  
游标的名称。 游标名必须符合有关标识符的规则。
  
'global'  
指定一个常量，该常量指示游标的源是一个全局游标名。
  
'variable'  
指定一个常量，该常量指示游标的源是一个本地变量。
  
*cursor_variable*  
游标变量的名称。 游标变量必须使用定义**光标**数据类型。
  
## <a name="return-types"></a>返回类型
**int**
  
|返回值|游标名|游标变量|  
|---|---|---|
|1|游标的结果集至少有一行。<br /><br /> 对于不区分的游标和键集游标，结果集至少有一行。<br /><br /> 对于动态游标，结果集可以有零行、一行或多行。|分配给该变量的游标已打开。<br /><br /> 对于不区分的游标和键集游标，结果集至少有一行。<br /><br /> 对于动态游标，结果集可以有零行、一行或多行。|  
|0|游标的结果集为空。*|分配给该变量的游标已经打开，然而结果集肯定为空。*|  
|-1|游标被关闭。|分配给该变量的游标被关闭。|  
|-2|不适用。|可以是：<br /><br /> 先前调用的过程并没有将游标分配给 OUTPUT 变量。<br /><br /> 先前调用的过程为 OUTPUT 变量分配了游标，然而在过程结束时，游标处于关闭状态。 因此，游标被释放，并且没有返回调用过程。<br /><br /> 没有将游标分配给已声明的游标变量。|  
|-3|具有指定名称的游标不存在。|具有指定名称的游标变量并不存在，或者即使存在这样一个游标变量，但并没有给它分配游标。|  
  
* 动态游标从不返回此结果。
  
## <a name="examples"></a>示例  
下面的示例使用 `CURSOR_STATUS` 函数显示游标在打开和关闭之前和之后的状态。
  
```sql
CREATE TABLE #TMP  
(  
   ii int  
)  
GO  
  
INSERT INTO #TMP(ii) VALUES(1)  
INSERT INTO #TMP(ii) VALUES(2)  
INSERT INTO #TMP(ii) VALUES(3)  
  
GO  
  
--Create a cursor.  
DECLARE cur CURSOR  
FOR SELECT * FROM #TMP  
  
--Display the status of the cursor before and after opening  
--closing the cursor.  
  
SELECT CURSOR_STATUS('global','cur') AS 'After declare'  
OPEN cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Open'  
CLOSE cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Close'  
  
--Remove the cursor.  
DEALLOCATE cur  
  
--Drop the table.  
DROP TABLE #TMP  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`After declare`
  
`---------------`
  
 `-1`  
  
`After Open`
  
`----------`
  
 `1`  
  
`After Close`
  
`-----------`
  
 `-1`  
  
## <a name="see-also"></a>另请参阅
[游标函数 &#40;Transact SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
  
  

