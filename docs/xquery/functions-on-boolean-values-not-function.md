---
title: not 函数（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: 8711190a6d3cbae0c716f7f62af478b70b9473e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038911"
---
# <a name="functions-on-boolean-values---not-function"></a>基于布尔值的函数 - not Function 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果 *$arg*的有效布尔值为 false，则返回 TRUE; 如果 *$Arg*的有效布尔值为 TRUE，则返回 false。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 具有有效布尔值一系列项。  
  
## <a name="examples"></a>示例  
 本主题提供了对存储在 AdventureWorks 数据库的各种**xml**类型列中的 xml 实例的 XQuery 示例。  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. 使用 not （） XQuery 函数查找其目录说明不包括规范> 元素的\<产品型号。  
 下面的查询将构造包含产品型号的 XML，该产品型号的目录说明中不包括 <`Specifications`> 元素。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
-   由于文档使用命名空间，因此示例将使用 WITH NAMESPACES 语句。 另一种方法是在[XQuery 序言](../xquery/modules-and-prologs-xquery-prolog.md)中使用**declare namespace**关键字来定义前缀。  
  
-   然后，该查询将构造包含 <`Product`> 元素及其**PRODUCTMODELID**属性的 XML。  
  
-   WHERE 子句使用[现有（）方法（XML 数据类型）](../t-sql/xml/exist-method-xml-data-type.md)来筛选行。 如果存在没有> 子元素\< \<规范的 ProductDescription> 元素，则**存在（）** 方法返回 True。 请注意**not （）** 函数的使用。  
  
 此结果集为空，因为每个产品型号目录说明都\<包括规范> 元素。  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. 使用 not() XQuery 函数检索没有 MachineHours 属性的生产车间  
 对 Instructions 列指定以下查询。 此列将存储产品型号的生产说明。  
  
 对于特殊的产品型号，查询将检索未指定 MachineHours 的生产车间。 也就是说，> 元素的**** \<位置未指定属性 MachineHours。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
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
  
-   [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)中的**Declarenamespace**定义艾德作品的生产说明命名空间前缀。 它表示在生产说明文档中使用了相同的命名空间。  
  
-   在查询中，如果没有**MachineHours**属性，则**not （@MachineHours）** 谓词返回 True。  
  
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
  
-   **Not （）** 函数仅支持类型为 xs： boolean、node （） * 或空序列的参数。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
