---
title: 有效的布尔值 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4ab470f5643335cd1ed26edd07aa93284bab1d47
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="effective-boolean-value-xquery"></a>有效的布尔值 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下面是有效的布尔值：  
  
-   如果操作数是空序列或布尔值 False，则为 False。  
  
-   否则，值为 True。  
  
 对于返回单个布尔值、节点序列或空序列的表达式，可以计算有效的布尔值。 请注意，在处理下列类型的表达式时，将隐式计算布尔值：  
  
-   逻辑表达式  
  
-   [上不起作用](../xquery/functions-on-boolean-values-not-function.md)  
  
-   FLWOR 表达式的 WHERE 子句  
  
-   [条件表达式](../xquery/conditional-expressions-xquery.md)  
  
-   [QuantifiedeExpressions](../xquery/quantified-expressions-xquery.md)  
  
 下面是有效的布尔值示例。 当**如果**处理表达式，可确定有效的布尔值的条件。 由于 `/a[1]` 返回空序列，因此有效的布尔值为 False。 结果以包含一个文本节点 (False) 的 XML 返回。  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 在以下示例中，由于表达式返回了非空序列，因此有效的布尔值为 True。  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 当查询类型化**xml**列或变量，你可以为 Boolean 类型的节点。 **Data （)** 在这种情况下返回一个布尔值。 如果查询表达式返回布尔值 True，则有效的布尔值为 True，如下例所示。 本例中对下列各项也进行了说明：  
  
-   创建一个 XML 架构集合。 元素\<b > 集合中是为 Boolean 类型。  
  
-   类型化**xml**变量会被创建并查询。  
  
-   表达式 `data(/b[1])` 返回布尔值 True。 因此，这种情况下，有效的布尔值为 True。  
  
-   表达式`data(/b[2])`返回一个布尔值 false 值。 因此，这种情况下，有效的布尔值为 False。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 基础知识](../xquery/xquery-basics.md)   
 [FLWOR 语句和迭代&#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
