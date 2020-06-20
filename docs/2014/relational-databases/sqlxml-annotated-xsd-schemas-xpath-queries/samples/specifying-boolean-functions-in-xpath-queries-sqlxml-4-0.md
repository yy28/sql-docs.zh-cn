---
title: 在 XPath 查询中指定布尔函数（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], Boolean functions
- false function
- not function [SQLXML]
- true function
- Boolean functions
ms.assetid: c72cd333-9294-4d41-84f2-1748bf20e3eb
author: rothja
ms.author: jroth
ms.openlocfilehash: 2318694767ceedfc3deffa925c90d235d115f1ca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062836"
---
# <a name="specifying-boolean-functions-in-xpath-queries-sqlxml-40"></a>在 XPath 查询中指定布尔函数 (SQLXML 4.0)
  以下示例说明如何在 XPath 查询中指定布尔函数。 这些示例中的 XPath 查询是针对 SampleSchema1.xml 中包含的映射架构指定的。 有关此示例架构的信息，请参阅[&#40;SQLXML 4.0&#41;的 XPath 批注的 XSD 架构示例](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>示例  
  
## <a name="a-specify-the-not-boolean-function"></a>A. 指定 not() 布尔函数  
 此查询返回 **\<Customer>** 不具有子元素的上下文节点的所有子元素 **\<Order>** ：  
  
```  
/child::Customer[not(child::Order)]  
```  
  
 `child` 轴为默认轴。 因此，可以将该查询指定为：  
  
```  
/Customer[not(Order)]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，并将其粘贴到文本文件中。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (BooleanFunctionsA.xml) 并将其保存到保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[not(Order)]  
    </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleSchema1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是执行该模板的部分结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
## <a name="b-specify-the-true-and-false-boolean-functions"></a>B. 指定 true() 和 false() 布尔函数  
 此查询返回 **\<Customer>** 不具有子元素的上下文节点的所有子元素 **\<Order>** 。 就关系而言，此查询返回未下订单的所有客户。  
  
```  
/child::Customer[child::Order=false()]  
```  
  
 `child` 轴为默认轴。 因此，可以将该查询指定为：  
  
```  
/Customer[Order=false()]  
```  
  
 此查询等效于以下内容：  
  
```  
/Customer[not(Order)]  
```  
  
 以下查询返回至少已下了一个订单的客户：  
  
```  
/Customer[Order=true()]  
```  
  
 此查询与下列代码功能等效：  
  
```  
/Customer[Order]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，并将其粘贴到文本文件中。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (BooleanFunctionsB.xml) 并将其保存到保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order=false()]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleSchema1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是执行该模板的部分结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
  
