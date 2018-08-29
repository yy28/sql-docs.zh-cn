---
title: 指导原则和限制的 XML 大容量加载 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 96f7a1296e45a333b5102c65f461358fd21b9893
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43059329"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大容量加载的指导原则和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在使用 XML 大容量加载时，您应该熟悉以下指导原则和限制：  
  
-   不支持内联架构。  
  
     如果在源 XML 文档中具有某一内联架构，则 XML 大容量加载将忽略该架构。 您为 XML 数据外部的 XML 大容量加载指定该映射架构。 不能通过使用指定映射架构针对节点**xmlns ="x： 架构"** 属性。  
  
-   将检查 XML 文档是否格式正确，但不对其进行验证。  
  
     XML 大容量加载检查 XML 文档以确定该文档的格式是否正确；即，确保 XML 符合万维网联合会的 XML 1.0 建议的语法要求。 如果该文档的格式不正确，则 XML 大容量加载将取消处理并返回错误。 对这一要求的唯一例外是在文档为片断时（例如，在文档没有单个根元素时），在此情况下 XML 大容量加载将加载文档。  
  
     XML 大容量加载不针对在 XML 数据文件中定义或引用的任何 XML 数据或 DTD 架构对文档进行验证。 此外，XML 大容量加载不针对提供的映射架构对 XML 数据文件进行验证。  
  
-   忽视所有 XML prolog 信息。  
  
     XML 大容量加载将忽略之前和之后的所有信息\<根 > XML 文档中的元素。 例如，XML 大容量加载将忽视所有 XML 声明、内部 DTD 定义、外部 DTD 引用和注释等。  
  
-   如果您具有定义两个表之间（例如 Customer 和 CustOrder 之间）的主键/外键关系的映射架构，则必须在该架构中首先描述具有主键的表。 具有外键列的表必须出现在该架构中的后面。 这样做的原因是，在架构中标识的表的顺序是用于加载到数据库中的顺序。例如，以下 XDR 架构将产生错误，使用在 XML 大容量加载中因为时**\<顺序 >** 之前描述元素**\<客户 >** 元素。 CustOrder 中的 CustomerID 列是引用 Cust 表中 CustomerID 主键列的外键列。  
  
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
  
-   如果架构未指定溢出列使用**sql:overflow-字段**批注，XML 大容量加载将忽略在 XML 文档中存在但未在映射架构中描述的任何数据。  
  
     XML 大容量加载只要在 XML 数据流中遇到已知标记，就会应用您指定的映射架构。 它将忽略在 XML 文档中提供、但未在该架构中描述的数据。 例如，假定您具有描述的映射架构**\<客户 >** 元素。 XML 数据文件具有 **\<AllCustomers >** 根标记 （它不在架构中描述） 包含所有**\<客户 >** 元素：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在这种情况下，XML 大容量加载将忽略 **\<AllCustomers >** 元素，并开始在映射**\<客户 >** 元素。 XML 大容量将加载忽略在该架构中未描述、但在 XML 文档中出现的元素。  
  
     包含的另一个 XML 源数据文件，请考虑**\<顺序 >** 元素。 以下元素在映射架构中未描述：  
  
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
  
     XML 大容量加载将忽略这些**\<顺序 >** 元素。 但是，如果您使用**sql:overflow-字段**批注架构中要为某列标识为溢出列，则 XML 大容量加载将所有未用完的数据存储在此列。  
  
-   CDATA 部分和实体引用在存储到数据库中之前将转换为等效的字符串。  
  
     在此示例中，CDATA 部分包装的值**\<城市 >** 元素。 XML 大容量加载中提取的字符串值 ("NY") 之前它将插入**\<城市 >** 到数据库中的元素。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大容量加载不保留实体引用。  
  
-   如果映射架构指定某一属性的默认值并且 XML 源数据不包含该属性，则 XML 大容量加载将使用该默认值。  
  
     以下示例 XDR 架构将分配到的默认值**HireDate**属性：  
  
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
  
     在此 XML 数据中， **HireDate**属性是从第二个丢失**\<客户 >** 元素。 当 XML 大容量加载插入第二个**\<客户 >** 到数据库中的元素，它使用在架构中指定的默认值。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   **Sql:url-编码**批注不支持：  
  
     无法在 XML 数据输入中指定某一 URL 后期望大容量加载从该位置读取数据。  
  
     创建在映射架构中标识的表（数据库必须存在）。 如果在数据库中已存在一个或多个表，SGDropTables 属性确定是否要删除并重新创建这些预先存在的表。  
  
-   如果指定 SchemaGen 属性 (例如，SchemaGen = true)，则创建在映射架构中标识的表。 但 SchemaGen 不会创建这些表上的任何约束 （例如，PRIMARY KEY/FOREIGN KEY 约束中） 有一个例外： 如果构成关系中的主键的 XML 节点被定义为具有 XML 类型的 ID (即，**类型 ="xsd:ID"** xsd) 和 SGUseID 属性设置为 True 的 SchemaGen，则不仅将创建从主键 ID 中输入了节点，但从映射架构关系创建主键/外键关系。  
  
-   SchemaGen 不使用 XSD 架构方面和扩展来生成关系[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]架构。  
  
-   如果指定 SchemaGen 属性 (例如，SchemaGen = true) 大容量加载，仅限表 （和不共享名称的视图） 指定的更新。  
  
-   SchemaGen 只提供用于从带批注的 XSD 生成关系架构的基本功能。 如果需要，用户应手动修改生成的表。  
  
-   SchemaGen 尝试创建包括两个表之间涉及的所有键的单个关系表之间存在多个关系的位置。 这一限制可能是由于 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 错误导致的。  
  
-   当您将 XML 数据大容量加载到某一数据库中时，在映射架构中必须至少有一个元素或子元素映射到某一数据库列。  
  
-   如果您在通过使用 XML 大容量加载插入数据值，则必须以 (-)CCYY-MM-DD((+-)TZ) 格式指定这些值。 这是针对日期的标准 XSD 格式。  
  
-   某些属性标志与其他属性标志不兼容。 例如，大容量加载不支持**Ignoreduplicatekeys = true**连同**Keepidentity = false**。 当**Keepidentity = false**，大容量加载需要服务器生成的密钥值。 表应具有**标识**键上的约束。 服务器将不生成重复键，这意味着无需**Ignoreduplicatekeys**设置为**true**。 **Ignoreduplicatekeys**应设置为**true**仅来自传入数据的主键值上载到表时，有行并且没有可能会发生冲突的主键值。  
  
  
