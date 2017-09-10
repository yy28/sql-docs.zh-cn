---
title: "ALTER FULLTEXT STOPLIST (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 314e41c5b885ee5441dbc4c88db14c22fc50e7b7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在当前数据库的默认全文非索引字表中插入或删除非索引字。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>参数  
 *stoplist_name*  
 要更改的非索引字表的名称。 *stoplist_name*最多 128 个字符。  
  
  *非索引字*   
 一个字符串，它可能是在指定的语言中具有语义的词或没有语义的标记。 *非索引字*仅限于令牌的最大长度 （64 个字符）。 非索引字可被指定为 Unicode 字符串。  
  
 语言*language_term*  
 指定要将与关联的语言*非索引字*正在添加或删除。  
  
 *language_term*可以指定为字符串、 整数或十六进制值对应于所选语言的区域设置标识符 (LCID)，如下所示：  
  
|格式|Description|  
|------------|-----------------|  
|字符串|*language_term*对应于**别名**中的列值[sys.syslanguages (TRANSACT-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)兼容性视图。 字符串必须括在单引号中，以作为在*language_term*。|  
|Integer|*language_term*是语言的 LCID。|  
|Hexadecimal|*language_term* 0x 后跟 LCID 的十六进制值。 十六进制值不能超过八位（包括前导零在内）。 如果该值是双字节字符集 (DBCS) 格式，则 SQL Server 将其转换为 Unicode 格式。|  
  
 添加*非索引字*语言*language_term*  
 将停止词添加到所指定语言的语言非索引字表*language_term*。  
  
 如果指定的关键字及语言 LCID 值组合在 STOPLIST 中不是唯一的，则将返回错误。  如果 LCID 值与已注册的语言不对应，则会产生一个错误。  
  
 删除 { *非索引字*语言*language_term* |所有语言*language_term* |所有}  
 从非索引字表中删除非索引字。  
  
  *非索引字* 语言*language_term*  
 删除所指定的语言指定的停止 word *language_term*。  
  
 所有语言*language_term*  
 删除所有指定的语言干扰词*language_term*。  
  
 ALL  
 删除非索引字表中的所有非索引字。  
  
## <a name="remarks"></a>注释  
 只有在兼容级别为 100 或更高时，才支持 CREATE FULLTEXT STOPLIST。 在 80 和 90 兼容级别下，会始终为数据库分配系统非索引字表。  
  
## <a name="permissions"></a>Permissions  
 若要将非索引字表指定为数据库的默认非索引字表，则需要 ALTER DATABASE 权限。 否则更改非索引字表需要非索引字表所有者或中的成员身份**db_owner**或**db_ddladmin**固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例将更改名为 `CombinedFunctionWordList` 的非索引字表，首先为西班牙语添加单词“en”，然后为法语添加单词“en”。  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建全文非索引字表 &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [为配置和管理非索引字和非索引字表的全文搜索](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [为全文搜索配置和管理非索引字和非索引字表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
