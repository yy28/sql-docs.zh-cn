---
title: "TEXTPTR (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs:
- TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84eaad80eff48689f91ab2679611d6eab6b2ce4d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="text-and-image-functions---textptr-transact-sql"></a>文本和图像函数-TEXTPTR (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回的文本指针值对应于**文本**， **ntext**，或**映像**中的列**varbinary**格式。 检索到的文本指针值可用于 READTEXT、WRITETEXT 和 UPDATETEXT 语句。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]没有可用的替代功能。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>参数  
 *列*  
 是**文本**， **ntext**，或**映像**将使用的列。  
  
## <a name="return-types"></a>返回类型  
 **varbinary**  
  
## <a name="remarks"></a>注释  
 对于含行内文本的表，TEXTPTR 将为要处理的文本返回一个句柄。 即使文本值为空，仍可获得有效的文本指针。  
  
 不能对视图列使用 TEXTPTR 函数。 只能对表列使用此函数。 若要在视图的列上使用 TEXTPTR 函数，你必须设置的兼容性级别为 80 使用[ALTER DATABASE 兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。 如果表没有行内文本，并且**文本**， **ntext**，或**映像**UPDATETEXT 语句尚未初始化列、 TEXTPTR 返回一个 null 指针。  
  
 可使用 TEXTVALID 来测试文本指针是否存在。 在没有有效的文本指针的情况下，不能使用 UPDATETEXT、WRITETEXT 或 READTEXT。  
  
 这些函数和语句也是有用当您使用时**文本**， **ntext**，和**映像**数据。  
  
|函数或语句|Description|  
|---------------------------|-----------------|  
|PATINDEX**(***%模式 %***，** *表达式***)**|返回指定的字符串的字符位置**文本**或**ntext**列。|  
|Datalength 之外**(***表达式***)**|返回中的数据长度**文本**， **ntext**，和**映像**列。|  
|SET TEXTSIZE|返回的限制，以字节为单位，**文本**， **ntext**，或**映像**与 SELECT 语句返回的数据。|  
|子字符串**(***text_column*，*启动*，*长度***)**|返回**varchar**指定由指定字符串*启动*偏移量和*长度*。 字符串的长度应小于 8 KB。|  
  
## <a name="examples"></a>示例  
  
> [!NOTE]  
>  若要运行下面的示例，必须安装**pubs**数据库。  
  
### <a name="a-using-textptr"></a>A. 使用 TEXTPTR  
 下面的示例使用`TEXTPTR`函数查找**映像**列`logo`与关联`New Moon Books`中`pub_info`表`pubs`数据库。 文本指针放在局部变量 `@ptrval.` 中。  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. 将 TEXTPTR 用于行内文本  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，必须在以下示例所示的事务中使用行内文本指针。  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. 返回文本数据  
 以下示例将从 `pub_id` 表中选择 `pr_info` 列和 `pub_info` 列的 16 字节文本指针。  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 以下示例显示如何在不使用 TEXTPTR 的情况下，返回文本的前 `8000` 个字节。  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. 返回特定文本数据  
 下面的示例查找`text`列 (`pr_info`) 与关联`pub_id``0736`中`pub_info`表`pubs`数据库。 该例首先声明了一个局部变量 `@val`。 然后，将文本指针（长二进制字符串）置于 `@val` 中，并将其作为参数提供给 `READTEXT` 语句。 结果将返回从第五个字节（偏移量为 4）开始的 10 个字节。  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [Datalength 之外 &#40;Transact SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT &#40;Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [设置 TEXTSIZE &#40;Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [文本和图像函数 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  

