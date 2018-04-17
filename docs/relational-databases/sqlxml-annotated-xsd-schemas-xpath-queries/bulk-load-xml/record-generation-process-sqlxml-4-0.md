---
title: 记录生成过程 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], record generation process
- node scopes [SQLXML]
- record subsets [SQLXML]
- scope [SQLXML]
- key ordering rules [SQLXML]
- record generation process for bulk loads [SQLXML]
- entering node scope [SQLXML]
- bulk load [SQLXML], record generation process
- leaving node scope [SQLXML]
- schema mapping [SQLXML]
ms.assetid: d8885bbe-6f15-4fb9-9684-ca7883cfe9ac
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e72388a753b1003c259f20371b34ffb3c269a2e1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="record-generation-process-sqlxml-40"></a>记录生成过程 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 大容量加载处理 XML 输入数据并为 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的相应表准备记录。 XML 大容量加载中的逻辑确定何时生成新记录、要将哪些子元素或属性值复制到记录的字段以及何时完成记录并可以发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以便插入。  
  
 XML 大容量加载不将整个 XML 输入数据加载到内存中，在将数据发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前不生成完整的记录集。 这是因为 XML 输入数据可能是大文档，将整个文档加载到内存代价过大。 XML 大容量加载改为执行以下操作：  
  
1.  分析映射架构并准备必要的执行计划。  
  
2.  将执行计划应用到输入流中的数据。  
  
 这种顺序处理使得按特定方式提供 XML 输入数据很重要。 您必须了解 XML 大容量加载是如何分析映射架构以及是如何生成记录的， 这样才能为 XML 大容量加载提供映射架构以生成您所要的结果。  
  
 XML 大容量加载处理常见映射架构批注，包括列和表映射（通过使用批注显式指定或通过默认映射隐式指定）以及联接关系。  
  
> [!NOTE]  
>  此处假定您熟悉带批注的 XSD 或 XDR 映射架构。 有关架构的详细信息，请参阅[简介批注 XSD 架构&#40;SQLXML 4.0&#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)或[批注 XDR 架构&#40;SQLXML 4.0 中弃用&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
 了解记录生成需要了解以下概念：  
  
-   节点作用域  
  
-   记录生成规则  
  
-   记录子集和键排序规则  
  
-   记录生成规则的例外情况  
  
## <a name="scope-of-a-node"></a>节点范围内  
 XML 文档中的节点 （一个元素或属性） 进入*纳入范围*XML 大容量加载在遇到时它在 XML 输入的数据流中。 对于元素节点，元素的开始标记使该元素进入作用域。 对于属性节点，属性名称使该属性进入作用域。  
  
 当在结束标记（对于元素节点）或属性值结尾（对于属性节点）没有更多数据用于节点时，则表示节点离开作用域。  
  
## <a name="record-generation-rule"></a>记录生成规则  
 节点（元素或属性）进入作用域时，可能从该节点生成记录。 只要相关的节点在作用域中，该记录就存在。 当节点离开作用域时，XML 大容量加载认为生成的记录已完成（带数据）并将它发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以便进行插入。  
  
 例如，考虑下面的 XSD 架构片段：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Customers" >  
   <xsd:complexType>  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
     <xsd:attribute name="CompanyName" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 该架构指定**\<客户 >**具有元素**CustomerID**和**CompanyName**属性。 **Sql:relation**批注地图**\<客户 >**到 Customers 表的元素。  
  
 考虑 XML 文档的以下片段：  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 将前文中所述的架构提供给 XML 大容量加载并使用 XML 数据作为输入，XML 大容量加载按以下方式处理源数据中的节点（元素和属性）：  
  
-   第一个开始标记**\<客户 >**元素会为该元素提供在作用域。 将此节点映射到 Customers 表。 因此，XML 大容量加载为 Customers 表生成一个记录。  
  
-   在架构中的所有属性， **\<客户 >**元素映射到的客户表的列。 这些属性进入作用域时，XML 大容量加载将它们的值复制到父作用域已生成的客户记录。  
  
-   XML 大容量加载在到达的结束标记**\<客户 >**元素，超出范围的元素。 这将导致 XML 大容量加载认为该记录已完成并将其发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 XML 大容量加载遵循此过程为每个后续**\<客户 >**元素。  
  
> [!IMPORTANT]  
>  在此模型中，由于是在到达结束标记（或节点离开作用域）时插入记录，因此必须定义节点作用域内与该记录相关的所有数据。  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>记录的子集和排序规则的密钥  
 如果指定使用的映射架构 **\<sql:relationship >**，子集术语是指在关系的外端生成的记录集。 在下面的示例中，CustOrder 记录位于外侧，  **\<sql:relationship >**。  
  
 例如，假定一个数据库包含以下各表：  
  
-   Cust (CustomerID, CompanyName, City)  
  
-   CustOrder (CustomerID, OrderID)  
  
 CustOrder 表中的 CustomerID 是外键，它引用 Cust 表中的 CustomerID 主键。  
  
 现在，请考虑在以下带批注的 XSD 架构中指定的 XML 视图。 此架构使用 **\<sql:relationship >**指定 Cust 和 CustOrder 表之间的关系。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 下面给出了示例 XML 数据和创建工作示例的步骤。  
  
-   当**\<客户 >** XML 数据文件中的元素节点就会进入作用域时，XML 大容量加载生成 Cust 表的记录。 XML 大容量加载然后必要的列的值 （CustomerID、 CompanyName 和 City） 将从复制 **\<CustomerID >**，  **\<CompanyName >**，和**\<城市 >**作为这些元素的子元素输入到作用域。  
  
-   当**\<顺序 >**元素节点就会进入作用域时，XML 大容量加载生成 CustOrder 表的记录。 XML 大容量加载操作将的值复制**OrderID**属性设为此记录。 从获取 CustomerID 列所需的值 **\<CustomerID >**的子元素**\<客户 >**元素。 XML 大容量加载使用中指定的信息 **\<sql:relationship >**来获取此记录的 CustomerID 外密钥值，除非**CustomerID**属性是指定在**\<顺序 >**元素。 常规规则是，如果子元素显式指定的外键属性的值，则 XML 大容量加载使用该值而不获取值从父元素通过使用指定 **\<sql:relationship >**. 与此**\<顺序 >**元素节点号超出范围时，XML 大容量加载发送到记录[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，然后处理所有后续**\<顺序 >**元素节点相同的方式。  
  
-   最后， **\<客户 >**元素节点号超出范围。 此时，XML 大容量加载将客户记录发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 XML 大容量加载为 XML 数据流中的所有后续客户执行此过程。  
  
 以下是有关映射架构的两点结论：  
  
-   当架构满足"包含"规则 (例如，关联的作用域内定义的所有数据与客户和订单的**\<客户 >**和 **\<顺序 >**元素节点)，大容量加载成功。  
  
-   在描述**\<客户 >**元素、 其子元素指定适当的顺序。 在这种情况下，  **\<CustomerID >**之前指定子元素**\<顺序 >**子元素。 这意味着，在输入的 XML 数据文件中，  **\<CustomerID >**元素值是可用作外键时值**\<顺序 >**元素进入到作用域。 首先指定键属性，此即“键排序规则”。  
  
     如果指定 **\<CustomerID >**子元素的后面**\<顺序 >**子元素，则这不可用 **\<顺序 >**元素进入到作用域。 当 **\</order >**然后读取结束标记，CustOrder 表的记录被视为完成，并使用 NULL 值不是所需的结果的 CustomerID 列的 CustOrder 表中插入。  
  
#### <a name="to-create-a-working-sample"></a>创建工作示例  
  
1.  将在该示例中提供的架构另存为 SampleSchema.xml。  
  
2.  创建这些表：  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                 OrderID        int         PRIMARY KEY,  
                 CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
3.  将以下示例 XML 输入数据另存为 SampleXMLData.xml：  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>   
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
        <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  若要执行 XML 大容量加载，请保存并执行以下 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) 示例 (BulkLoad.vbs)：  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
## <a name="exceptions-to-the-record-generation-rule"></a>记录生成规则的例外情况  
 如果节点属于 IDREF 或 IDREFS 类型，则在它进入作用域时，XML 大容量加载不为该节点生成记录。 您必须确保在架构的同一位置存在记录的完整描述。 **Dt: type ="nmtokens"**批注将被忽略，就像忽略 IDREFS 类型。  
  
 例如，考虑下面的 XSD 架构描述**\<客户 >**和**\<顺序 >**元素。 **\<客户 >**元素包括**OrderList** IDREFS 类型的属性。  **\<Sql:relationship >**标记指定的客户和订单的列表之间的一个对多关系。  
  
 以下是架构：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
                 parent="Cust"  
                 parent-key="CustomerID"  
                 child="CustOrder"  
                 child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="CompanyName" type="xsd:string" />  
    <xsd:attribute name="City" type="xsd:string" />  
    <xsd:attribute name="OrderList"   
                       type="xsd:IDREFS"   
                       sql:relation="CustOrder"   
                       sql:field="OrderID"  
                       sql:relationship="CustCustOrder" >  
    </xsd:attribute>  
  </xsd:complexType>  
 </xsd:element>  
  
  <xsd:element name="Order" sql:relation="CustOrder" >  
   <xsd:complexType>  
    <xsd:attribute name="OrderID" type="xsd:string" />  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="OrderDate" type="xsd:date" />  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 因为大容量加载将忽略 IDREFS 类型的节点，则不记录生成时**OrderList**属性节点就会进入作用域。 如果要将订单记录添加到 Orders 表，必须在架构中的某个地方描述这些订单。 在此架构中，指定**\<顺序 >**元素可确保 XML 大容量加载将订单记录添加到订单表。 **\<顺序 >**元素描述填充 CustOrder 表的记录所需的所有属性。  
  
 你必须确保**CustomerID**和**OrderID**中值**\<客户 >**元素中的值匹配 **\<顺序 >**元素。 由您负责维护引用完整性。  
  
#### <a name="to-test-a-working-sample"></a>测试工作示例  
  
1.  创建这些表：  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
                  CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
                  CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID),  
                  OrderDate      datetime DEFAULT '2000-01-01')  
    GO  
    ```  
  
2.  将在该示例中提供的映射架构另存为 SampleSchema.xml。  
  
3.  将以下示例 XML 数据另存为 SampleXMLData.xml：  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1111" CompanyName="Sean Chai" City="NY"  
                 OrderList="Ord1 Ord2" />  
      <Customers CustomerID="1112" CompanyName="Dont Know" City="LA"  
                 OrderList="Ord3 Ord4" />  
      <Order OrderID="Ord1" CustomerID="1111" OrderDate="1999-01-01" />  
      <Order OrderID="Ord2" CustomerID="1111" OrderDate="1999-02-01" />  
      <Order OrderID="Ord3" CustomerID="1112" OrderDate="1999-03-01" />  
      <Order OrderID="Ord4" CustomerID="1112" OrderDate="1999-04-01" />  
    </ROOT>  
    ```  
  
4.  若要执行 XML 大容量加载，请保存并执行此 VBScript 示例 (SampleVB.vbs)：  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
