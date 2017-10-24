---
title: "-（注释） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a03aff79db25c07fc828145177e29196405a9264
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="---comment-transact-sql"></a>--（注释）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  表示用户提供的文本。 可以将注释插入单独行中，嵌套在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令行的结尾或嵌套在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中。 服务器不对注释进行计算。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>参数  
 *text_of_comment*  
 是包含注释的文本的字符字符串。  
  
## <a name="remarks"></a>注释  
 将两个连字符 (--) 用于单行或嵌套的注释。 用 -- 插入的注释由换行符终止。 注释没有最大长度限制。 下表列出了可用来注释或取消注释文本的键盘快捷键：  
  
|操作|Standard|  
|------------|--------------|  
|将选定文本设为注释|Ctrl+K、Ctrl+C|  
|取消注释所选文本|Ctrl+K、Ctrl+U|  
  
 有关键盘快捷方式的详细信息，请参阅[SQL Server Management Studio 键盘快捷键](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)。  
  
 多行注释，请参阅[正斜杠星型注释 &#40;Transact SQL &#41;](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>示例  
 下面的示例使用 -- 注释字符。  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

