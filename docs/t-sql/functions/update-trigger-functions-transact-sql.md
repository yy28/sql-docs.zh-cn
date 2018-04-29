---
title: UPDATE() (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UPDATE()_TSQL
- UPDATE()
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], UPDATE function
- testing column updates
- UPDATE function
- UPDATE() function
- detecting changes
- columns [SQL Server], change detection
- UPDATE statement [SQL Server], UPDATE function
- verifying column updates
- checking column updates
ms.assetid: 8e3be25b-2e3b-4d1f-a610-dcbbd8d72084
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b91d175788e3f67e8a4e4cc1484e9648072c4cef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="update---trigger-functions-transact-sql"></a>UPDATE - 触发器函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个布尔值，指示是否尝试对表或视图的指定列执行 INSERT 或 UPDATE 操作。 可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 或 UPDATE 触发器主体中的任意位置使用 UPDATE()，以测试触发器是否应执行某些操作。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>参数  
 *column*  
 要为 INSERT 或 UPDATE 操作测试的列的名称。 由于表名是在触发器的 ON 子句中指定的，因此不要在列名前包含表名。 列可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的任何[数据类型](../../t-sql/data-types/data-types-transact-sql.md)。 但是，计算列不能用于此上下文。  
  
## <a name="return-types"></a>返回类型  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 UPDATE() 返回 TRUE，不考虑 INSERT 或 UPDATE 尝试是否成功。  
  
 若要测试对多个列执行的 INSERT 或 UPDATE 操作，请在第一个操作后指定单独的 UPDATE(column) 子句。 通过使用 COLUMNS_UPDATED，也可以为 INSERT 或 UPDATE 操作测试多个列。 这会返回一个位模式，指示插入或更新的列。  
  
 在 INSERT 操作中，IF UPDATE 将返回 TRUE 值，因为这些列插入了显式值或隐式 (NULL) 值。  
  
> [!NOTE]  
>  IF UPDATE(column)子句的功能等同于 IF、IF...ELSE 或 WHILE 子句，并且可以使用 BEGIN...END 语句块。 有关详细信息，请参阅[控制流语言 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)。  
  
 可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 触发器主体中的任意位置使用 UPDATE(column)。  
  
## <a name="examples"></a>示例  
 以下示例创建一个触发器；当有人尝试更新 `StateProvinceID` 表的 `PostalCode` 或 `Address` 列时，该触发器将向客户端输出一条消息。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [COLUMNS_UPDATED (Transact-SQL)](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
