---
title: "本地名称函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 52ae1021c17469e8fb5691fcf1da527cc348c950
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="functions-on-nodes---local-name"></a>在节点的本地名称的函数
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回的名称的本地部分*$arg*为 xs: string 将是零长度字符串，或将有 xs:NCName 词法窗体。 如果未提供参数，默认值为上下文节点。  
  
## <a name="syntax"></a>语法  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将检索其本地名称部分的节点名称。  
  
## <a name="remarks"></a>注释  
  
-   在 SQL Server， **fn:local-name()**没有仅可以依赖于上下文的谓词的上下文中使用的参数。 特别要指出的是，它只能在方括号 (`[ ]`) 内使用。  
  
-   如果提供了参数而参数是空序列，则该函数返回长度为零的字符串。  
  
-   如果目标节点没有名称（因为它是文档节点、注释或文本节点），该函数返回长度为零的字符串。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. 检索特定节点的本地名称  
 下面的查询是针对非类型化的 XML 实例指定的。 查询表达式 `local-name(/ROOT[1])` 检索指定节点的本地名称部分。  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 以下查询是针对 ProductModel 表的 Instructions 列（一个类型化的 xml 列）指定的。 表达式 `local-name(/AWMI:root[1]/AWMI:Location[1])` 返回指定节点的本地名称 `Location`。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. 在谓词中使用不带参数的本地名称  
 下面的查询指定针对 Instructions 列中，键入**xml**的 ProductModel 表的列。 表达式返回其 QName 的本地名称部分为“Location”的 <`root`> 元素的所有元素子级。 **Local-name()**函数为指定谓词中的，并且它由该功能使用的上下文节点没有自变量。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 该查询返回 <`root`> 元素的所有 <`Location`> 元素子级。  
  
## <a name="see-also"></a>另请参阅  
 [在节点上的函数](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [命名空间 uri 函数 &#40;XQuery &#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
