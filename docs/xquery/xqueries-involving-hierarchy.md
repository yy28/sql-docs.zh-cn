---
title: 涉及层次结构的 XQueries |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
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
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dd9e93969bd8677311edc22ae61f314c8b89c5d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="xqueries-involving-hierarchy"></a>涉及层次结构的 XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  大多数**xml**类型中的列**AdventureWorks**数据库是半结构化的文档。 因此，每行中存储的文档可能看起来不同。 本主题中的查询示例说明如何从这些不同的文档提取信息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. 从生产说明文档检索生产车间以及这些生产车间的第一个生产步骤  
 对于产品型号 7，查询将构造 XML 包含 <`ManuInstr`> 元素，与**ProductModelID**和**ProductModelName**特性，和一个或多个 <`Location`>子元素。  
  
 每个 <`Location`> 元素具有它自己的属性集和一个 <`step`> 子元素。 此 <`step`> 子元素是生产车间的第一个生产步骤。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   **命名空间**中的关键字[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)定义命名空间前缀。 随后，将在查询正文中使用此前缀。  
  
-   上下文切换标记 {) 和 (} 用于将查询从 XML 构造切换到查询计算。  
  
-   **Sql:column()** 用于正在构造的 XML 中包含的关系的值。  
  
-   在构造 <`Location`> 元素时，$wc/@* 将检索所有生产车间属性。  
  
-   **String （)** 函数返回的字符串值从 <`step`> 元素。  
  
 下面是部分结果：  
  
```  
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. 在 AdditionalContactInfo 列中查找所有电话号码  
 下面的查询通过在整个层次结构中搜索 <`telephoneNumber`> 元素来检索用于联系特定客户的附加电话号码。 因为 <`telephoneNumber`> 元素可以出现在层次结构中任何位置，所以该查询在搜索中使用后代和自身运算符 (//)。  
  
```  
SELECT AdditionalContactInfo.query('  
 declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 结果如下：  
  
```  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 若要只检索顶级电话号码（即 <`AdditionalContactInfo`> 的 <`telephoneNumber`> 子元素），查询中的 FOR 表达式应变为  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`中创建已分区表或索引。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 基础知识](../xquery/xquery-basics.md)   
 [XML 构造&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [XML 数据 (SQL Server)](../relational-databases/xml/xml-data-sql-server.md)  
  
  
