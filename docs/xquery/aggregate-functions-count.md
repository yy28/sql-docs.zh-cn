---
title: count 函数 (XQuery) |Microsoft 文档
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
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9e995026b8690f4254f8f4db357874bbd2fa833b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835595"
---
# <a name="aggregate-functions---count"></a>聚合函数 - count
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回指定的序列中包含的项数目 *$arg*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 要计数的项。  
  
## <a name="remarks"></a>备注  
 如果将返回 0 *$arg*是一个空序列。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. 使用 count() XQuery 函数计算产品型号生产中的生产车间数。  
 以下查询将计算产品型号 (ProductModelID=7) 生产过程中的生产车间数。  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   **命名空间**中的关键字[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)定义命名空间前缀。 该前缀随后将用于 XQuery 主体。  
  
-   此查询将构造包含 <`NoOfWorkStations`> 元素的 XML。  
  
-   **Count （)** 函数，在 XQuery 正文计数的数量 <`Location`> 元素。  
  
 结果如下：  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 您还可以构造包含产品型号 ID 和名称的 XML，如以下查询所示：  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 结果如下：  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 可以将这些值作为非 xml 类型（而不是 xml 类型）返回，如以下查询所示。 该查询使用[value （） 方法 （xml 数据类型）](../t-sql/xml/value-method-xml-data-type.md)要检索的工作中心位置计数。  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 结果如下：  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
