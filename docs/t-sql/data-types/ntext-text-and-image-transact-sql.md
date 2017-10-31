---
title: "ntext、 text 和 image (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ntext_TSQL
- ntext
dev_langs:
- TSQL
helpviewer_keywords:
- text data type, about text data type
- text [SQL Server], data types
- ntext data type
- ntext data type, about ntext data type
- image data type, about image data type
ms.assetid: b0d8769c-7598-4f97-8162-ace5f182b5bc
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 76b78b01596b484bc35df1a1e468c5b2bb8ece63
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="ntext-text-and-image-transact-sql"></a>ntext、text 和 image (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

用于存储大型非 Unicode 字符、Unicode 字符及二进制数据的固定长度数据类型和可变长度数据类型。 Unicode 数据使用 UNICODE UCS-2 字符集。
  
>**重要说明！**  **ntext**，**文本**，和**映像**将 SQL Server 的未来版本中删除数据类型。 请避免在新开发工作中使用这些数据类型，并考虑修改当前使用这些数据类型的应用程序。 请改用 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)、 [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)和 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) 。  
  
  
## <a name="arguments"></a>参数  
**ntext**  
长度可变的 Unicode 数据，字符串最大长度为 2^30 - 1 (1,073,741,823) 个字节。 存储大小是所输入字符串长度的两倍（以字节为单位）。 ISO 同义词**ntext**是**国家/地区文本**。
  
**text**  
服务器代码页中长度可变的非 Unicode 数据，字符串最大长度为 2^31-1 (2,147,483,647) 个字节。 当服务器代码页使用双字节字符时，存储仍是 2,147,483,647 字节。 根据字符串，存储大小可能小于 2,147,483,647 字节。
  
**image**  
长度可变的二进制数据，从 0 到 2^31-1 (2,147,483,647) 个字节。
  
## <a name="remarks"></a>注释  
可以使用以下函数和语句**ntext**，**文本**，或**映像**数据。
  
|函数|语句|  
|---|---|
|[Datalength 之外 &#40;Transact SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)|[READTEXT &#40;Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)|[设置 TEXTSIZE &#40;Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[子字符串 &#40;Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)|[UPDATETEXT &#40;Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40;Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40;Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)


