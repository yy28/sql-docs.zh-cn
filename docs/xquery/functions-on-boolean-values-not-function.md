---
title: "not 函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f64f286b59b67e31d0b49527a83409b81ba2210
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-boolean-values---not-function"></a>对布尔值的函数上不起作用 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果返回 TRUE 的有效布尔值*$arg*为 false，否则，返回 FALSE 的有效布尔值*$arg*为 true。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 具有有效布尔值一系列项。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. 不包括使用 not() XQuery 函数查找其目录说明的产品型号\<规范 > 元素。  
 以下查询将为目录说明中不包括 <`Specifications`> 元素的产品型号构造包含产品型号 ID 的 XML。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 请注意上述查询的以下方面：  
  
-   由于文档使用命名空间，因此示例将使用 WITH NAMESPACES 语句。 另一个选项是使用**声明命名空间**中的关键字[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)定义前缀。  
  
-   该查询然后构造的 XML，包括 <`Product`> 元素并将其**ProductModelID**属性。  
  
-   WHERE 子句使用[exist （） 方法 （XML 数据类型）](../t-sql/xml/exist-method-xml-data-type.md)的行进行过滤。 **Exist （)**方法返回 True，如果有\<ProductDescription > 元素不具有\<规范 > 子元素。 请注意，使用**not()**函数。  
  
 该结果集为空，因为每个产品型号目录说明包括\<规范 > 元素。  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. 使用 not() XQuery 函数检索没有 MachineHours 属性的生产车间  
 对 Instructions 列指定以下查询。 此列将存储产品型号的生产说明。  
  
 对于特殊的产品型号，查询将检索未指定 MachineHours 的生产车间。 也就是说，该属性**MachineHours**没有为指定\<位置 > 元素。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 在上述查询中，请注意以下内容：  
  
-   **Declarenamespace**中[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)定义生产说明命名空间前缀 Adventure Works。 它表示在生产说明文档中使用了相同的命名空间。  
  
-   在查询中，**不 (@MachineHours)**谓词返回 True，如果没有任何**MachineHours**属性。  
  
 结果如下：  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Not()**函数仅支持类型 xs: boolean，或 node （） * 或空序列的自变量。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
