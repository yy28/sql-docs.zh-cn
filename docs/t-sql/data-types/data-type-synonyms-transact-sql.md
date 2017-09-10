---
title: "数据类型的同义词 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1d9b1da2bdc7084268740cd7de2580e64ee9698b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-synonyms-transact-sql"></a>数据类型的同义词 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中包含数据类型同义词以便实现 ISO 兼容性。 下表列出了这些同义词以及它们映射到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型。
  
|同义词|SQL Server 系统数据类型|  
|---|---|
|**不同的二进制**|**varbinary**|  
|**不同的 char**|**varchar**|  
|**字符**|**char**|  
|**字符**|**char （1)**|  
|**字符 (**  *n*  **)**|**char(n)**|  
|**不同的字符 (**  *n*  **)**|**varchar(n)**|  
|**年 12 月**|**decimal**|  
|**双精度**|**float**|  
|**float**[**(***n***)**] 为 *n*  = 1-7|**real**|  
|**float**[**(***n***)**] 为 *n*  = 8-15|**float**|  
|**integer**|**int**|  
|**国家/地区字符 (**  *n*  **)**|**nchar （n)**|  
|**国家/地区 char (**  *n*  **)**|**nchar （n)**|  
|**不同的国家/地区字符 (**  *n*  **)**|**nvarchar （n)**|  
|**不同的国家/地区 char (**  *n*  **)**|**nvarchar （n)**|  
|**国家/地区的文本**|**ntext**|  
|**timestamp**|rowversion|  
  
数据类型同义词可以代替中数据定义语言 (DDL) 语句，如创建表，创建过程中，相应的基本数据类型名，或声明 *@variable* 。 但是，创建对象后看不到同义词。 创建对象后，为对象分配与同义词相关联的基本数据类型。 没有记录能表明在创建对象的语句中指定了同义词。
  
将给所有由原始对象派生出的对象（如结果集列或表达式）分配基本数据类型。 所有对原始对象和任何派生对象执行的后续元数据函数都将报告基本数据类型，而不是同义词。 出现此行为元数据操作，如**sp_help**和其他系统存储过程、 信息架构视图或报告表或结果集中的数据类型的各种数据访问 API 元数据操作列。
  
例如，您可以通过指定 `national character varying` 创建表：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`实际上被分配**nvarchar(10)**数据类型和所有后续的元数据函数将报告作为列**nvarchar(10)**列。 元数据函数将永远不会报告它们作为**国家字符集 varying(10)**列。
  
## <a name="see-also"></a>另请参阅
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
  
  

