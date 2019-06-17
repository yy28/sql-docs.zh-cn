---
title: 标识键列使用 sql:key 的字段 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc3c063da7bb9133f8687a908c4bd7e0e13bae8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013823"
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>使用 sql:key-fields 标识键列 (SQLXML 4.0)
  针对 XSD 架构指定 XPath 查询时，大多数情况下必须有键信息才能获得结果中的正确嵌套。 指定 `sql:key-fields` 批注是一种确保生成正确层次结构的方式。  
  
> [!NOTE]  
>  若要确保正确的嵌套，建议您为映射到表的元素指定 `sql:key-fields`。 所生成的 XML 对于基础结果集的排序敏感。 如果不指定 `sql:key-fields`，则所生成的 XML 的格式可能不正确。  
  
 `sql:key-fields` 的值用于标识唯一标识关系中的行的列。 如果需要多个列才能唯一标识某行，则用空格分隔列值。  
  
 必须使用`sql:key-fields`批注如果元素包含 **\<sql: relationship >** 的元素和子元素之间定义，但不提供在指定的表的主键父元素中。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. 生成正确的嵌套时\<sql: relationship > 未提供足够信息  
 该示例显示必须指定 `sql:key-fields` 的地方。  
  
 请考虑以下架构。 该架构指定的层次结构之间 **\<顺序 >** 并 **\<客户 >** 元素在其中 **\<顺序 >** 元素是父元素和 **\<客户 >** 元素是子元素。  
  
 **\<Sql: relationship >** 标记用于指定父-子关系。 它将 Sales.SalesOrderHeader 表中的 CustomerID 标识为父键，该父键引用 Sales.Customer 表中的 CustomerID 子键。 中提供的信息 **\<sql: relationship >** 不足以唯一标识父表 (Sales.SalesOrderHeader) 中的行。 因此，如果没有 `sql:key-fields` 批注，则生成的层次结构不准确。  
  
 与`sql:key-fields`上指定 **\<顺序 >** 、 批注可唯一标识父 （Sales.SalesOrderHeader 表） 中的行和及其子元素出现其父级的下方。  
  
 以下是架构：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>创建此架构的工作示例  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 KeyFields1.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 KeyFields1.xml 的相同目录中将该文件另存为 KeyFields1T.xml。 模板中的 XPath 查询返回所有 **\<顺序 >** customerid 小于 3 的元素。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (KeyFields1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 查询](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分结果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. 指定 sql:key-fields 以便在结果中生成正确的嵌套  
 在以下架构中，没有使用指定的层次结构 **\<sql: relationship >** 。 此架构仍然需要指定 `sql:key-fields` 批注才能唯一标识 HumanResources.Employee 表中的雇员。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>创建此架构的工作示例  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 KeyFields2.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 KeyFields2.xml 的相同目录中将该文件另存为 KeyFields2T.xml。 模板中的 XPath 查询返回所有 **\<HumanResources.Employee >** 元素：  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (KeyFields2.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 查询](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是结果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
