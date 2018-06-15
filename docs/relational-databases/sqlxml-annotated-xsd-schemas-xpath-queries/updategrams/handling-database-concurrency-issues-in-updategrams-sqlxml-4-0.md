---
title: 处理 Updategram (SQLXML 4.0) 中的数据库并发问题 |Microsoft 文档
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
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73ae79d0831820366f5ec6454573df26c7b36e01
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973132"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>在 Updategram 中处理数据库并发问题 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  与其他数据库更新机制一样，updategram 必须处理多用户环境下对数据的并发更新。 Updategram 使用乐观并发控制，该模式将选择字段数据与快照进行比较，以确保要更新的数据自从在数据库中读取后，其他用户应用程序未更改过该数据。 Updategram 包括这些快照值**\<之前 >** updategram 的块。 在更新数据库之前, 属的 updategram 检查中指定的值**\<之前 >** 块针对当前中数据库后，以确保更新是有效的值。  
  
 乐观并发控制在 updategram 中提供三种保护级别：低（无）、中间和高。 通过相应指定 updategram，可以确定需要的保护级别。  
  
## <a name="lowest-level-of-protection"></a>最低保护级别  
 此级别为盲目更新，它不参照自上次读取数据库后已进行的其他更新来处理更新。 在这种情况下，指定仅在主键列**\<之前 >** 阻止来标识记录，并指定中的更新的信息**\<后 >** 块。  
  
 例如，无论以前的电话号码是什么，以下 updategram 中的新联系人电话号码都是正确的。 请注意如何**\<之前 >** 块指定仅的主键列 (ContactID)。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>中间保护级别  
 在此保护级别中，updategram 将要更新的数据的当前值与数据库列中的值进行比较，以确保自您的事务读取记录后，这（个）些值未被任何其他事务更改过。  
  
 你可以通过指定主键列和要更新中的列中获取此级别的保护**\<之前 >** 块。  
  
 例如，此 updategram 为 ContactID 是 1 的联系人更新 Person.Contact 表的 Phone 列中的值。 **\<之前 >** 块指定**Phone**属性以确保此属性的值，然后再应用更新后的值匹配数据库中的相应列中的值.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>高保护级别  
 高保护级别确保自您的应用程序上次读取该记录后该记录没有变化（即自您的应用程序读取记录后，该记录未被任何其他事务更改过）。  
  
 可以通过两种方法实现针对并发更新的此类高保护级别：  
  
-   指定的表中的其他列**\<之前 >** 块。  
  
     如果你指定中的其他列**\<之前 >** 块，属的 updategram 的应用更新前已在数据库中的值与这些列指定的值进行比较。 如果自您的事务读取记录后有记录列被更改过，updategram 将不执行更新。  
  
     例如，以下属的 updategram 更新 shift 名称，但指定其他列 （StartTime 和 EndTime） 中**\<之前 >** 块，这要求更高级别的针对并发的保护更新。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     此示例通过指定所有列中的记录的值指定最高级别的保护**\<之前 >** 块。  
  
-   在指定时间戳列 （如果可用） **\<之前 >** 块。  
  
     而不是指定中的所有记录列**\<之前**> 块中，你可以只需指定时间戳列 （如果表有一个） 以及主键列在**\<之前>** 块。 在每次更新记录后，数据库将时间戳列更新为唯一值。 在这种情况下，updategram 将时间戳的值与数据库中的相应值进行比较。 在数据库中存储的时间戳值为二进制值。 因此，必须为架构中指定的时间戳列**dt:type="bin.hex"**， **dt:type="bin.base64"**，或**sql: datatype ="timestamp"**。 (你可以指定**xml**数据类型或[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。)  
  
#### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  创建此表中的**tempdb**数据库：  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  添加此示例记录：  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  复制以下 XSD 架构并将其粘贴到记事本中。 将其另存为 ConcurrencySampleSchema.xml：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  将以下 updategram 代码复制到记事本中，然后在保存上一步中创建的架构的相同目录中将其保存为 ConcurrencySampleTemplate.xml。 （请注意下面 LastUpdated 的时间戳值将不同于示例 Customer 表中的值，因此从表中复制 LastUpdated 的实际值并将其粘贴到 updategram。）  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 这是等效的 XDR 架构：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>另请参阅  
 [属的 Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
