---
title: "指导原则和限制的 XML 大容量加载 (SQLXML 4.0) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 453ce7fe955af4ffe25d13b1ab1abfef0f48cf59
ms.sourcegitcommit: 7673ad0e84a6de69420e19247a59e39ca751a8aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2018
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大容量加载的指导原则和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]当使用 XML 大容量加载时，你应该熟悉以下指导原则和限制：  
  
-   不支持内联架构。  
  
     如果在源 XML 文档中具有某一内联架构，则 XML 大容量加载将忽略该架构。 您为 XML 数据外部的 XML 大容量加载指定该映射架构。 你无法通过使用指定节点的映射架构**xmlns ="x： 架构"**属性。  
  
-   将检查 XML 文档是否格式正确，但不对其进行验证。  
  
     XML 大容量加载检查 XML 文档以确定该文档的格式是否正确；即，确保 XML 符合万维网联合会的 XML 1.0 建议的语法要求。 如果该文档的格式不正确，则 XML 大容量加载将取消处理并返回错误。 对这一要求的唯一例外是在文档为片断时（例如，在文档没有单个根元素时），在此情况下 XML 大容量加载将加载文档。  
  
     XML 大容量加载不针对在 XML 数据文件中定义或引用的任何 XML 数据或 DTD 架构对文档进行验证。 此外，XML 大容量加载不针对提供的映射架构对 XML 数据文件进行验证。  
  
-   忽视所有 XML prolog 信息。  
  
     XML 大容量加载将忽略之前和之后的所有信息\<根 > XML 文档中的元素。 例如，XML 大容量加载将忽视所有 XML 声明、内部 DTD 定义、外部 DTD 引用和注释等。  
  
-   如果您具有定义两个表之间（例如 Customer 和 CustOrder 之间）的主键/外键关系的映射架构，则必须在该架构中首先描述具有主键的表。 具有外键列的表必须出现在该架构中的后面。 这样做的原因是，在其中架构中所标识的表的顺序是用于将它们加载到数据库的顺序。例如，下面的 XDR 架构将产生错误，使用在 XML 大容量加载因为时**\<顺序 >**元素进行了描述之前**\<客户 >**元素。 CustOrder 中的 CustomerID 列是引用 Cust 表中 CustomerID 主键列的外键列。  
  
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
  
-   如果架构未指定溢出列使用**sql:overflow-字段**批注，XML 大容量加载将忽略 XML 文档中存在，但在映射架构中不会对其进行描述的任何数据。  
  
     XML 大容量加载只要在 XML 数据流中遇到已知标记，就会应用您指定的映射架构。 它将忽略在 XML 文档中提供、但未在该架构中描述的数据。 例如，假定你将描述的映射架构**\<客户 >**元素。 XML 数据文件具有 **\<AllCustomers >**根标记 （它不在架构中描述） 包含所有**\<客户 >**元素：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在这种情况下，将忽略 XML 大容量加载 **\<AllCustomers >**元素，并开始在映射**\<客户 >**元素。 XML 大容量将加载忽略在该架构中未描述、但在 XML 文档中出现的元素。  
  
     请考虑包含的另一个 XML 源数据文件**\<顺序 >**元素。 以下元素在映射架构中未描述：  
  
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
  
     XML 大容量加载将忽略这些**\<顺序 >**元素。 但是，如果你使用**sql:overflow-字段**中要一个列标识为溢出列中，XML 大容量加载的架构的批注将所有未用完的数据存储在此列。  
  
-   CDATA 部分和实体引用在存储到数据库中之前将转换为等效的字符串。  
  
     在此示例中，CDATA 部分包装的值**\<城市 >**元素。 XML 大容量加载提取的字符串值 ("NY")，则会插入之前**\<城市 >**元素插入数据库。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大容量加载不保留实体引用。  
  
-   如果映射架构指定某一属性的默认值并且 XML 源数据不包含该属性，则 XML 大容量加载将使用该默认值。  
  
     下面的示例 XDR 架构分配默认值为**HireDate**属性：  
  
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
  
     在此 XML 数据， **HireDate**属性是从第二个丢失**\<客户 >**元素。 XML 大容量加载时插入第二个**\<客户 >**到数据库的元素，它使用架构中指定的默认值。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   **Sql:url-编码**批注不支持：  
  
     无法在 XML 数据输入中指定某一 URL 后期望大容量加载从该位置读取数据。  
  
     创建在映射架构中标识的表（数据库必须存在）。 如果数据库中已存在一个或多个表，SGDropTables 属性确定是否要删除并重新创建这些预先存在的表。  
  
-   如果指定 SchemaGen 属性 (例如，SchemaGen = true)，创建了在映射架构中标识的表。 但 SchemaGen 不会创建这些表 （如为主键/外键约束中） 的任何约束有一个例外： 如果为具有 XML 类型的 ID 定义构成关系中的主键的 XML 节点 (即，**类型 ="xsd:ID"** xsd) 和 SGUseID 属性设置为 True 时 SchemaGen，则不仅将创建从主键 ID 类型化节点，但从映射关系的架构创建主键/外键关系。  
  
-   SchemaGen 不使用 XSD 架构方面和扩展来生成关系[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]架构。  
  
-   如果指定 SchemaGen 属性 (例如，SchemaGen = true) on Bulk Load，仅限表 （和不的共享名称的视图） 指定的更新。  
  
-   SchemaGen 仅提供从批注 XSD 生成关系架构的基本功能。 如果需要，用户应手动修改生成的表。  
  
-   在表之间存在多个关系 SchemaGen 尝试创建含有涉及两个表之间的所有密钥的单个关系。 这一限制可能是由于 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 错误导致的。  
  
-   当您将 XML 数据大容量加载到某一数据库中时，在映射架构中必须至少有一个元素或子元素映射到某一数据库列。  
  
-   如果您在通过使用 XML 大容量加载插入数据值，则必须以 (-)CCYY-MM-DD((+-)TZ) 格式指定这些值。 这是针对日期的标准 XSD 格式。  
  
-   某些属性标志与其他属性标志不兼容。 例如，大容量加载不支持**Ignoreduplicatekeys = true**连同**Keepidentity = false**。 当**Keepidentity = false**，大容量加载需要服务器以生成密钥的值。 表应具有**标识**此项上的约束。 服务器将不会生成重复键，意味着无需**Ignoreduplicatekeys**将设置为**true**。 **Ignoreduplicatekeys**应设置为**true**仅上载到表中的传入数据的主键值时，有行以及有可能会发生冲突的主键值。  
  
  
