---
title: XML 大容量加载的指导原则和限制（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 593e51e34be3b607af121bfcba92497e019eba3f
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703382"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大容量加载的指导原则和限制 (SQLXML 4.0)
  在使用 XML 大容量加载时，您应该熟悉以下指导原则和限制：  
  
-   不支持内联架构。  
  
     如果在源 XML 文档中具有某一内联架构，则 XML 大容量加载将忽略该架构。 您为 XML 数据外部的 XML 大容量加载指定该映射架构。 不能使用**xmlns = "x:schema"** 属性在节点上指定映射架构。  
  
-   将检查 XML 文档是否格式正确，但不对其进行验证。  
  
     XML 大容量加载检查 XML 文档以确定该文档的格式是否正确，即确保 XML 符合万维网联合会的 XML 1.0 建议的语法要求。 如果该文档的格式不正确，则 XML 大容量加载将取消处理并返回错误。 对这一要求的唯一例外是在文档为片断时（例如，在文档没有单个根元素时），在此情况下 XML 大容量加载将加载文档。  
  
     XML 大容量加载不针对在 XML 数据文件中定义或引用的任何 XML 数据或 DTD 架构对文档进行验证。 此外，XML 大容量加载不针对提供的映射架构对 XML 数据文件进行验证。  
  
-   忽视所有 XML prolog 信息。  
  
     XML 大容量加载将忽略 \< xml 文档中根> 元素之前和之后的所有信息。 例如，XML 大容量加载将忽视所有 XML 声明、内部 DTD 定义、外部 DTD 引用和注释等。  
  
-   如果您具有定义两个表之间（例如 Customer 和 CustOrder 之间）的主键/外键关系的映射架构，则必须在该架构中首先描述具有主键的表。 具有外键列的表必须出现在该架构中的后面。 这样做的原因是，架构中的表标识顺序是用于将它们加载到数据库中的顺序。例如，下面的 XDR 架构将在 XML 大容量加载中使用时产生错误，因为在** \< Customer>** 元素之前介绍了** \< Order>** 元素。 CustOrder 中的 CustomerID 列是引用 Cust 表中 CustomerID 主键列的外键列。  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   如果该架构未通过使用 `sql:overflow-field` 批注指定溢出列，则 XML 大容量加载将忽略在 XML 文档中提供、但未在该映射架构中描述的所有数据。  
  
     XML 大容量加载只要在 XML 数据流中遇到已知标记，就会应用您指定的映射架构。 它将忽略在 XML 文档中提供、但未在该架构中描述的数据。 例如，假设您有一个映射架构，该架构描述了一个** \< Customer>** 元素。 XML 数据文件具有包含所有** \< 客户>** 元素的** \< AllCustomers>** 根标记（在架构中未介绍）：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在这种情况下，XML 大容量加载将忽略** \< AllCustomers>** 元素，并在** \< Customer>** 元素处开始映射。 XML 大容量将加载忽略在该架构中未描述、但在 XML 文档中出现的元素。  
  
     请考虑另一个 XML 源数据文件，其中包含** \< Order>** 元素。 以下元素在映射架构中未描述：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     XML 大容量加载将忽略这些** \< 顺序>** 元素。 但是，如果在 `sql:overflow-field` 架构中使用批注将列标识为溢出列，则 XML 大容量加载会将所有未用完的数据存储在此列中。  
  
-   CDATA 部分和实体引用在存储到数据库中之前将转换为等效的字符串。  
  
     在此示例中，CDATA 节包装** \< City>** 元素的值。 XML 大容量加载在将** \< City>** 元素插入到数据库中之前提取字符串值（"NY"）。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大容量加载不保留实体引用。  
  
-   如果映射架构指定某一属性的默认值并且 XML 源数据不包含该属性，则 XML 大容量加载将使用该默认值。  
  
     下面的示例 XDR 架构将默认值分配给 "**雇佣**日期" 属性：  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     在此 XML 数据中，第二个** \< 客户>** 元素中缺少 "**雇佣**日期" 属性。 当 XML 大容量加载将第二个** \< 客户>** 元素插入到数据库中时，它将使用在该架构中指定的默认值。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   不支持 `sql:url-encode` 批注：  
  
     无法在 XML 数据输入中指定某一 URL 后期望大容量加载从该位置读取数据。  
  
     创建在映射架构中标识的表（数据库必须存在）。 如果数据库中已存在一个或多个表，则 SGDropTables 属性将确定是否删除并重新创建这些预先存在的表。  
  
-   如果指定 SchemaGen 属性（例如，SchemaGen = true），则将创建在映射架构中标识的表。 但是，SchemaGen 不会在这些表中创建任何约束（如主键/外键约束），但有一个例外：如果构成关系中的主键的 XML 节点定义为具有 XML 类型 ID （即， `type="xsd:ID"` 对于 XSD），且 SGUseID 属性设置为 True （对于 SchemaGen），则不仅是从 ID 类型化节点创建主键，而且还从映射架构关系创建主键/外键关系。  
  
-   SchemaGen 不使用 XSD 架构方面和扩展来生成关系 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 架构。  
  
-   如果在大容量加载时指定 SchemaGen 属性（例如，SchemaGen = true），则只会更新指定的表（而不是共享名称的视图）。  
  
-   SchemaGen 仅提供用于从带批注的 XSD 生成关系架构的基本功能。 如果需要，用户应手动修改生成的表。  
  
-   在表之间存在多个关系的情况下，SchemaGen 会尝试创建单个关系，其中包括这两个表之间涉及的所有键。 这一限制可能是由于 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 错误导致的。  
  
-   当您将 XML 数据大容量加载到某一数据库中时，在映射架构中必须至少有一个元素或子元素映射到某一数据库列。  
  
-   如果您在通过使用 XML 大容量加载插入数据值，则必须以 (-)CCYY-MM-DD((+-)TZ) 格式指定这些值。 这是针对日期的标准 XSD 格式。  
  
-   某些属性标志与其他属性标志不兼容。 例如，大容量加载不支持 `Ignoreduplicatekeys=true` 与 `Keepidentity=false` 一起使用。 在 `Keepidentity=false` 时，大容量加载需要服务器生成键值。 表对该键应该具有 `IDENTITY` 约束。 服务器将不生成重复键，这意味着无需将 `Ignoreduplicatekeys` 设置为 `true`。 只有在将来自传入数据的主键值上载到具有多行的表中且这些主键值可能存在冲突时，`Ignoreduplicatekeys` 才应设置为 `true`。  
  
  
