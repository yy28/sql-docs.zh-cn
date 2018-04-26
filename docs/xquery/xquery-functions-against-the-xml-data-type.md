---
title: 对 xml 数据类型的 XQuery 函数 |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 53ca81622f07103e40cfce6950979a69b0f4a623
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="xquery-functions-against-the-xml-data-type"></a>针对 xml 数据类型的 XQuery 函数
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主题及其副主题描述你可以使用的指定 XQuery 时函数**xml**数据类型。 有关 W3C 规范中，请参阅[ http://www.w3.org/TR/2004/WD-xpath-functions-20040723 ](http://go.microsoft.com/fwlink/?LinkId=4873)。  
  
 XQuery 函数属于http://www.w3.org/2004/07/xpath-functions命名空间。 W3C 规范使用“fn:”命名空间前缀来说明这些函数。 使用这些函数时，不必显式指定“fn:”命名空间前缀。 由于这个原因，也为了提高可读性，此文档中通常不使用命名空间前缀。  
  
 下表列出针对支持的 XQuery 函数**xml**数据类型。  
  
|类别|函数名称|  
|--------------|-------------------|  
|[基于数值的函数](http://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[上限](../xquery/numeric-values-functions-ceiling.md)|  
||[floor](../xquery/numeric-values-functions-floor.md)|  
||[舍入](../xquery/numeric-values-functions-round.md)|  
|[对字符串值的 XQuery 函数](http://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[concat](../xquery/functions-on-string-values-concat.md)|  
||[包含](../xquery/functions-on-string-values-contains.md)|  
||[子字符串](../xquery/functions-on-string-values-substring.md)|  
||[小写函数&#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[字符串长度](../xquery/functions-on-string-values-string-length.md)|  
||[大写函数&#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|对布尔值的函数|[不](../xquery/functions-on-boolean-values-not-function.md)|  
|[在节点上的函数](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[number](../xquery/functions-on-nodes-number.md)|  
||[本地名称函数 (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[命名空间 uri 函数 (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[上下文函数](http://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[最后一个](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[在序列上的函数](http://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[为空](../xquery/functions-on-sequences-empty.md)|  
||[非重复值](../xquery/functions-on-sequences-distinct-values.md)|  
||[id 函数 (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[聚合函数&#40;XQuery&#41;](http://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[计数](../xquery/aggregate-functions-count.md)|  
||[avg](../xquery/aggregate-functions-avg.md)|  
||[最小值](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[总和](../xquery/aggregate-functions-sum.md)|  
|[构造函数&#40;XQuery&#41;](../xquery/constructor-functions-xquery.md)|[构造函数](../xquery/constructor-functions-xquery.md)|  
|[数据取值函数](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[布尔构造函数&#40;XQuery&#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[true 函数 (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false 函数 (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[函数与 QNames &#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[展开的 QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[本地-名称-从的 QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[命名空间的 uri-从的 QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[SQL Server XQuery 扩展函数](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[sql:column() 函数 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[sql: variable 函数 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>另请参阅  
 [xml 数据类型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)   
 [XML 数据 (SQL Server)](../relational-databases/xml/xml-data-sql-server.md)  
  
  
