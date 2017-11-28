---
title: "TRIGGER_NESTLEVEL (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRIGGER_NESTLEVEL
- TRIGGER_NESTLEVEL_TSQL
dev_langs: TSQL
helpviewer_keywords:
- triggers [SQL Server], number executed
- number of triggers
- TRIGGER_NESTLEVEL function
ms.assetid: 6a33e74a-0cf9-4ae1-a1e4-4a137a3ea39d
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0416b80079ac4c1dfb6dc10b507fd85800dd3a27
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="triggernestlevel-transact-sql"></a>TRIGGER_NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回为激发触发器的语句执行的触发器数。 TRIGGER_NESTLEVEL 在 DML 和 DDL 触发器中用以确定当前的嵌套级别。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
## <a name="arguments"></a>参数  
 *object_id*  
 触发器的对象 ID。 如果*object_id*指定，则返回该语句已执行指定的触发器的次数。 如果*object_id*未指定，则执行的所有触发器返回语句的次数。  
  
  *trigger_type*   
 指定将 TRIGGER_NESTLEVEL 应用于 AFTER 触发器还是 INSTEAD OF 触发器。 指定**AFTER**的 AFTER 触发器。 指定**IOT** INSTEAD OF 触发器。 如果*trigger_type*指定，则*trigger_event_category*还必须指定。  
  
  *trigger_event_category*   
 指定将 TRIGGER_NESTLEVEL 应用于 DML 触发器还是 DDL 触发器。 指定**DML** DML 触发器。 指定**DDL**用于 DDL 触发器。 如果*trigger_event_category*指定，则*trigger_type*还必须指定。 请注意，只有**AFTER**可通过指定**DDL**，这是因为 DDL 触发器只能 AFTER 触发器。  
  
## <a name="remarks"></a>注释  
 如果未指定参数，则 TRIGGER_NESTLEVEL 返回调用堆栈上的触发器总数。 这包括它本身。 当触发器所执行的命令导致其他触发器激发，或导致触发器的连续激发时，可省略参数。  
  
 若要在特定触发器类型和事件类别的调用堆栈上返回触发器的总数，指定*object_id* = 0。  
  
 如果 TRIGGER_NESTLEVEL 在触发器的外部执行，且任何参数均不为 NULL，则 TRIGGER_NESTLEVEL 返回 0。  
  
 如果将任何参数显式指定为 NULL，则无论在触发器内部还是外部使用 TRIGGER_NESTLEVEL，都将返回值 NULL。  
  
## <a name="examples"></a>示例  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>A. 测试特定 DML 触发器的嵌套级别  
  
```  
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>B. 测试特定 DDL 触发器的嵌套级别  
  
```  
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>C. 测试执行的所有触发器的嵌套级别  
  
```  
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
