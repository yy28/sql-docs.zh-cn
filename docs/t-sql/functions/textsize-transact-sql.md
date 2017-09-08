---
title: "@@TEXTSIZE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TEXTSIZE'
- '@@TEXTSIZE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, TEXTSIZE option
- SELECT statement [SQL Server], text size returned
- TEXTSIZE option
- '@@TEXTSIZE function'
- text size returned [SQL Server]
ms.assetid: 4308a7b9-8e8f-49e9-8246-8224e32f4953
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2525b2cfea6130dba7b84ff918260969738f994
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="textsize-transact-sql"></a>@@TEXTSIZE (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回的当前值[TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md)选项。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@TEXTSIZE  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="examples"></a>示例  
 下面的示例使用`SELECT`以显示`@@TEXTSIZE`值之前和之后更改与`SET``TEXTSIZE`语句。  
  
```  
-- Set the TEXTSIZE option to the default size of 4096 bytes.  
SET TEXTSIZE 0  
SELECT @@TEXTSIZE AS 'Text Size'  
SET TEXTSIZE 2048  
SELECT @@TEXTSIZE AS 'Text Size'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text Size`  
  
 `-----------`  
  
 `4096`  
  
 `Text Size`  
  
 `-----------`  
  
 `2048`  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [设置 TEXTSIZE &#40;Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)  
  
  
