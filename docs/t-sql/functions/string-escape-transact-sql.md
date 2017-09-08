---
title: "STRING_ESCAPE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f969e292eff76c9a836ccd3177519d88e355ac
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在文本中的特殊字符进行转义，并返回带有转义字符的文本。 **STRING_ESCAPE**是确定性函数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>参数  
 *text*  
 是**nvarchar**[表达式](../../t-sql/language-elements/expressions-transact-sql.md)表示应进行转义的对象的表达式。  
  
 *type*  
 将应用的转义规则。 目前支持的值是`'json'`。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar (max)**带有转义的特殊和控制字符的文本。 当前**STRING_ESCAPE**仅转义 JSON 中的以下表所示的特殊字符。  
  
|特殊字符|编码的序列|  
|-----------------------|----------------------|  
|引号 (")|\\"|  
|反斜线号 (\\)|\\\|  
|斜线号 （/）|\\/|  
|退格键|\b|  
|换页符|\f|  
|换行符|\n|  
|回车符|\r|  
|水平制表符|\t|  
  
|控制字符|编码的序列|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  转义根据格式设置规则的 JSON 文本  
 以下查询使用 JSON 规则的特殊字符进行转义，并返回转义的文本。  
  
```  
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `escapedText`  
  
 `-------------------------------------------------------------`  
  
 `\\\t\/\n\\\\\t\"\t`  
  
### <a name="b-format-json-object"></a>B. 格式 JSON 对象  
 下面的查询创建 JSON 文本，并从数字和字符串变量，并在变量中的任何特殊 JSON 字符进行转义。  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>另请参阅  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [子字符串 &#40;Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

