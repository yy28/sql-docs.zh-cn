---
title: local-name 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 93f289ed165742ae8fdf8d49732186161a4a8b5d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666986"
---
# <a name="functions-on-nodes---local-name"></a>基于节点的函数 - local-name
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回的名称的本地部分 *$arg*为 xs: string 的将是零长度字符串或 xs: ncname 的词汇形式。 如果未提供参数，默认值为上下文节点。  
  
## <a name="syntax"></a>语法  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将检索其本地名称部分的节点名称。  
  
## <a name="remarks"></a>备注  
  
-   在 SQL Server 中， **fn:local-name()** 没有仅可以使用上下文相关的谓词的上下文中的参数。 特别要指出的是，它只能在方括号 (`[ ]`) 内使用。  
  
-   如果提供了参数而参数是空序列，则该函数返回长度为零的字符串。  
  
-   如果目标节点没有名称（因为它是文档节点、注释或文本节点），该函数返回长度为零的字符串。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
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
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. 在谓词中使用不带参数的本地名称  
 针对类型化的 Instructions 列指定下面的查询**xml** ProductModel 表的列。 表达式返回其 QName 的本地名称部分为“Location”的 <`root`> 元素的所有元素子级。 **Local-name （)** 函数在谓词中的指定了，并且它的函数使用上下文节点没有参数。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 该查询返回 <`root`> 元素的所有 <`Location`> 元素子级。  
  
## <a name="see-also"></a>请参阅  
 [基于节点的函数](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [命名空间 uri 函数&#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
