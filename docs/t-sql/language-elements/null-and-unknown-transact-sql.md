---
title: "NULL 和未知 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdac1899707b3caa4f4c515324511a47830f2722
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="null-and-unknown-transact-sql"></a>NULL 和未知 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL 指示的值是未知。 Null 值是不同的空或零值。 没有两个相等的空值。 比较两个 null 值，之间或 null 值和任何其他值，之间返回未知的因为每个空的值是未知。  
  
 Null 值通常指示数据是未知、 不适用，或要在以后添加。 例如，客户的中间名首字母在客户下定单时可能不知道。  
  
 请注意下列有关 null 值：  
  
-   若要在查询中测试空值，请在 WHERE 子句中使用 IS NULL 或 IS NOT NULL。  
  
-   通过显式声明在 INSERT 或 UPDATE 语句中的 NULL 或离开从 INSERT 语句的列，null 值可以插入到列。  
  
-   作为将表中的一个行与在表中，如主键，或者用于分发行，例如分发键的信息的另一个行区分开来所需的信息不能使用 null 值。  
  
 如果数据中出现空值，则逻辑运算符和比较运算符有可能返回 TRUE 或 FALSE 以外的第三种结果 UNKNOWN。 这种对三值逻辑的需要是导致许多应用程序出错的根源。 下面这些表概括了引入空值比较的效果。  
  
 下表显示应用于两个布尔操作数和运算符的结果，其中一个操作数，则返回 NULL。  
  
|操作数 1|操作数 2|结果|  
|---------------|---------------|------------|  
|TRUE|NULL|FALSE|  
|NULL|NULL|FALSE|  
|FALSE|NULL|FALSE|  
  
 下表显示应用于两个布尔操作数或运算符的结果，其中一个操作数，则返回 NULL。  
  
|操作数 1|操作数 2|结果|  
|---------------|---------------|------------|  
|TRUE|NULL|TRUE|  
|NULL|NULL|UNKNOWN|  
|FALSE|NULL|UNKNOWN|  
  
## <a name="see-also"></a>另请参阅  
 [和 &#40;Transact SQL &#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [或者 &#40;Transact SQL &#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [不 &#40;Transact SQL &#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [为 NULL &#40;Transact SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  

