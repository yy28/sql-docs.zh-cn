---
title: 构造函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2ce2bc5e905fe4fa8bd204c850d29b1fa0fdadb0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780065"
---
# <a name="constructor-functions-xquery"></a>构造函数 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从指定的输入中，构造函数创建任意 XSD 内置或用户定义原子类型的实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>参数  
 *$strval*  
 将被转换的字符串。  
  
 *TYP*  
 任意内置 XSD 类型。  
  
## <a name="remarks"></a>备注  
 支持用于基本和派生原子 XSD 类型的构造函数。 但是的子**xs: duration**，其中包括**xdt: yearmonthduration 和 xdt: daytimeduration**，并**xs: qname**， **xs: nmtoken**，并**xs: notation**不受支持。 倘若它们是直接或间接从以下类型中派生的，则相关联的架构集合中提供的用户定义原子类型也可用。  
  
#### <a name="supported-base-types"></a>支持的基类型  
 以下是所支持的基类型：  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>支持的派生类型  
 以下是所支持的派生类型：  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 SQL Server 也以以下方式支持构造函数调用的常量折叠：  
  
-   如果参数为字符串文字，则将在编译期间计算表达式。 当该值不满足类型约束时，将生成静态错误。  
  
-   如果参数为其他类型的文字，将在编译期间计算表达式。 当该值不满足类型约束时，将返回空序列。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. 使用 dateTime() XQuery 函数检索以前的产品说明  
 在此示例中，示例 XML 文档首先分配给**xml**类型的变量。 此文档包含三个示例 <`ProductDescription`> 元素，每个元素都包含一个 <`DateCreated`> 子元素。  
  
 然后，查询该变量以便仅检索在特定日期之前创建的那些产品说明。 为了进行比较，该查询使用**xs:dateTime()** 构造函数键入日期。  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 请注意上述查询的以下方面：  
  
-   FOR ...WHERE 循环结构用于检索\<ProductDescription > 满足 WHERE 子句中指定的条件元素。  
  
-   **Datetime （)** 构造函数用于构造**dateTime**类型值，因此可以进行适当比较。  
  
-   然后，该查询将构造得到的 XML。 由于构造一系列属性，因此在 XML 构造中要使用逗号和括号。  
  
 结果如下：  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 构造&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
