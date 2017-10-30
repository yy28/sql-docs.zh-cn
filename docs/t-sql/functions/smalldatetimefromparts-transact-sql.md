---
title: "SMALLDATETIMEFROMPARTS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 0f561d37aae876f94946c8210665f642daec9755
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  返回**smalldatetime**值的指定的日期和时间。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
## <a name="arguments"></a>参数  
 *年*  
 用于指定年度的整数表达式。  
  
 *月*  
 用于指定月份的整数表达式。  
  
 *一天*  
 用于指定日期的整数表达式。  
  
 *小时*  
 用于指定小时的整数表达式。  
  
 *分钟*  
 用于指定分钟的整数表达式。  
  
## <a name="return-types"></a>返回类型  
 **smalldatetime**  
  
## <a name="remarks"></a>注释  
 此函数可以充当完全初始化的构造函数**smalldatetime**值。 如果自变量不是有效的将引发错误。 如果所需的参数为 null，则返回 null。  
  
 此函数可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器以及更高版本上远程执行。 不到具有以下版本的服务器进行远程处理[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
## <a name="examples"></a>示例  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  


