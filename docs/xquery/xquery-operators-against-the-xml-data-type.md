---
title: XQuery 运算符反对 xml 数据类型 |微软文档
description: 了解可用于 xml 数据类型的 XQuery 运算符。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
ms.openlocfilehash: d5692aa5b46d79c68165fa6f1320034fdb7e03b3
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388303"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>针对 xml 数据类型的 XQuery 运算符
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 支持下列运算符：  
  
-   数字运算符（+、-、*、div、mod）  
  
-   值比较运算符（eq、ne、lt、gt、le、ge）  
  
-   用于一般比较的运算符 （*，！=，>，*，>\< \<= ）  
  
 有关这些运算符的详细信息，请参阅[比较表达式&#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-general-operators"></a>A. 使用一般运算符  
 此查询说明了应用于序列和比较序列的一般运算符的使用方法。 查询从**联系人**表的 **"附加联系人信息"** 列中检索每个客户的电话号码序列。 然后，将这个序列与两个电话号码（“111-111-1111”、“222-2222”）序列进行比较。  
  
 查询使用**=** 比较运算符。 **=** 将运算符右侧序列中的每个节点与左侧序列中的每个节点进行比较。 如果节点匹配，则节点比较为**TRUE**。 然后将其转换为整数并与 1 进行比较，然后查询将返回客户 ID。  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 还有另一种方法可以观察前一个查询的工作原理：从 **"附加联系人信息"** 列检索的每个电话号码值与两个电话号码集进行比较。 如果该值处于集中，则该客户将返回到结果中。  
  
### <a name="b-using-a-numeric-operator"></a>B. 使用数字运算符  
 此查询中的运算符 + 是一个值运算符，因为它应用于单个项。 例如，将值 1 添加到查询返回的许多大小值上：  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. 使用值运算符  
 以下查询检索图片大小为"`Picture`小"的产品模型<>元素：  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 由于**eq**运算符的两个操作数都是原子值，因此在查询中使用值运算符。 可以使用常规比较运算符 （）**=** 编写相同的查询。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [XML 数据&#40;SQL 服务器&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)  
  
  
