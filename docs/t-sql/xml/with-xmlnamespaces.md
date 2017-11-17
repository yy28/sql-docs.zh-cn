---
title: "WITH XMLNAMESPACES (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs:
- TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34d67133c083c0dba5325548971997e8b95d6c5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  声明一个或多个 XML 命名空间。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>参数  
 *xml_namespace_uri*  
 统一资源标识符 (URI)，用于标识正在声明的 XML 命名空间。 *xml_namespace_uri*为 SQL 字符串。  
  
 *xml_namespace_prefix*  
 指定要映射和中指定的命名空间 URI 值相关联的前缀*xml_namespace_uri*。 *xml_namespace_prefix*必须[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符。  
  
## <a name="remarks"></a>注释  
 在还包括公用表表达式的语句中使用 WITH XMLNAMESPACES 子句时，WITH XMLNAMESPACES 子句必须位于语句中的公用表表达式的前面。  
  
 下面是在使用 WITH XMLNAMESPACES 子句时所应用的常规语法规则：  
  
-   每个 XML 命名空间声明都必须包含至少一个 XML 默认命名空间声明项。  
  
-   所使用的每个 XML 命名空间前缀都必须是非移植名称 (NCName)，在这样的名称中冒号字符 (:) 不是名称的一部分。  
  
-   不能两次定义同一个命名空间前缀。  
  
-   XML 命名空间前缀和 URI 是区分大小写的。  
  
-   不能声明 XML 命名空间前缀 `xmlns`。  
  
-   除了命名空间 URI `xml` 以及不能为其分配不同前缀的此 URI 以外，不能用其他命名空间覆盖 XML 命名空间前缀 `'http://www.w3.org/XML/1998/namespace'`。  
  
-   当查询正在使用 ELEMENTS XSINIL 指令时，不能重新声明 XML 命名空间前缀 `xsi`。  
  
-   URI 字符串值按照当前数据库排序规则代码页进行编码，并且将内部转换为 Unicode。  
  
-   XML 命名空间 URI 将空白折叠以下 XSD 空白折叠规则用于**xs: anyuri**。 另外，不会对 XML 命名空间 URI 值执行实体化和反实体化。  
  
-   系统将检查 XML 命名空间 URI 中是否有无效的 XML 1.0 字符，如果发现这样的字符（例如，U+0007），将引发错误。  
  
-   XML 命名空间 URI（折叠所有空格后）不能是零长度的字符串，否则会发生“无效的空命名空间 URI”错误。  
  
-   XMLNAMESPACES 关键字保留在 WITH 子句的上下文中。  
  
## <a name="examples"></a>示例  
 有关示例，请参阅[将命名空间添加到查询使用 WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 语言参考 (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)  
  
  

