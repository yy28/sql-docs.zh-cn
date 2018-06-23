---
title: 在 XPath 查询 (SQLXML 4.0) 中指定算术运算符 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- arithmetic operators
- XPath operators [SQLXML]
- XPath queries [SQLXML], arithmetic operators
- operators [SQLXML]
ms.assetid: fdfbc87d-759f-4abc-acf5-a21de01f78d3
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4fe4e247041306cfd00854ae021e2fb5ec64c0b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123577"
---
# <a name="specifying-arithmetic-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查询中指定算数运算符 (SQLXML 4.0)
  以下示例说明如何在 XPath 查询中指定算数运算符。 本示例中的 XPath 查询针对 SampleSchema1.xml 中包含的映射架构指定。 有关此示例架构的信息，请参阅[有关 XPath 示例的示例批注 XSD 架构&#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-specify-the--arithmetic-operator"></a>A. 指定 * 算数运算符  
 此 XPath 查询返回 **\<OrderDetail >** 满足指定谓词的元素：  
  
```  
/child::OrderDetail[@UnitPrice * @Quantity = 12.350]  
```  
  
 在查询中，`child`是轴和`OrderDetail`是节点的测试 (true **OrderDetail**是**\<元素节点 >**，这是因为 **\<元素 >** 节点是主节点进行`child`轴)。 所有 **\<OrderDetail >** 元素节点，则应用谓词中的测试，并且返回那些满足条件的节点。  
  
> [!NOTE]  
>  XPath 中的数字是双精度浮点数，对本示例中的浮点数进行比较将导致舍入。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)并将其粘贴到文本文件。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (ArithmeticOperatorA.xml)，并将它保存在保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /OrderDetail[@UnitPrice * @OrderQty = 12.350]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleSchema1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
```  
Here is the partial result set of the template execution:    
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-710" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
   ...  
</ROOT>  
```  
  
  