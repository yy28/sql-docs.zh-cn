---
title: "授予对 XML 架构集合的权限 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- granting permissions [SQL Server], XML schema collections
- ALTER permission
ms.assetid: ffbb829c-3b8f-4e5d-97d9-ab4059aab0db
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7c89c6a8322e8922a7d0a2d59ea686a2d703947a
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="grant-permissions-on-an-xml-schema-collection"></a>授予对 XML 架构集合的权限
  您可以授予创建 XML 架构集合的权限，也可以授予对 XML 架构集合对象的某些操作权限。  
  
## <a name="granting-permission-to-create-an-xml-schema-collection"></a>授予创建 XML 架构集合的权限  
 若要创建 XML 架构集合，必须具有下列权限：  
  
-   主体必须具有数据库级的 CREATE XML SCHEMA COLLECTION 权限。  
  
-   由于 XML 架构集合是关系架构作用域对象，因此主体还必须具有对关系架构的 ALTER 权限。  
  
 下列权限使主体可以在服务器数据库中的关系架构中创建 XML 架构集合：  
  
-   对服务器具有 CONTROL 权限  
  
-   对服务器具有 ALTER ANY DATABASE 权限  
  
-   对数据库具有 ALTER 权限  
  
-   数据库中的 CONTROL 权限  
  
-   数据库中的 ALTER ANY SCHEMA 权限和 CREATE XML SCHEMA COLLECTION 权限  
  
-   对关系架构具有 ALTER 或 CONTROL 权限以及数据库中的 CREATE XML SCHEMA COLLECTION 权限  
  
 在下面的示例中使用了最后一种权限方法。  
  
 关系架构的所有者将变成在该架构中创建的 XML 架构集合的所有者。 这样，此所有者就可以完全控制 XML 架构集合。 因此，此所有者就可以修改 XML 架构集合、类型化 xml 列或删除 XML 架构集合。  
  
## <a name="granting-permissions-on-an-xml-schema-collection-object"></a>授予对 XML 架构集合对象的某些操作权限  
 允许对 XML 架构集合具有下列权限：  
  
-   当使用 ALTER XML SCHEMA COLLECTION 语句修改现有 XML 架构集合的内容时，必须具有 ALTER 权限。  
  
-   CONTROL 权限使用户可以对 XML 架构集合执行任何操作。  
  
-   若要将 XML 架构集合的所有权从一个主体传递到另一个主体，必须具有 TAKE OWNERSHIP 权限。  
  
-   REFERENCES 权限可授权主体使用 XML 架构集合来类型化或约束表和视图中的 **xml** 类型列以及参数。 当一个 XML 架构集合引用另一个 XML 架构集合时，也必须具有 REFERENCES 权限。  
  
-   如果主体对 XML 架构集合具有 ALTER、REFERENCES 或 CONTROL 权限之一，则 VIEW DEFINITION 权限就使此主体能够通过 XML_SCHEMA_NAMESPACE 或目录视图来查询该集合的内容。  
  
-   若要验证主体针对类型化或约束 **xml** 类型列、变量和参数的 XML 架构集合插入或更新的值，必须具有 EXECUTE 权限。 当查询存储在这些列和变量中的 XML 时，也必须具有此权限。  
  
## <a name="examples"></a>示例  
 以下示例中的应用场景说明 XML 架构权限的工作机制。 每个示例都创建有必需的测试数据库、关系架构和登录帐户。 这些登录帐户已授予必需的 XML 架构集合权限。 每个示例均在结束时进行了必要的清除。  
  
### <a name="a-granting-permissions-to-create-an-xml-schema-collection"></a>A. 授予创建 XML 架构集合的权限  
 下面的示例显示如何授予权限以便主体能够创建 XML 架构集合。 此示例将创建一个示例数据库和一个测试用户 `TestLogin1`。 `TestLogin1` 针对关系架构的 `ALTER` 权限和针对数据库的 `CREATE XML SCHEMA COLLECTION` 权限。 有了这些权限， `TestLogin1` 便可以成功创建示例 XML 架构集合。  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Execute CREATE XML SCHEMA COLLECTION.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="root" type="xsd:byte"/>  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-granting-permission-to-use-an-existing-xml-schema-collection"></a>B. 授予使用现有 XML 架构集合的权限  
 以下示例将进一步显示针对 XML 架构集合的权限模式。 该示例将显示创建和使用 XML 架构集合时需要哪些不同的权限。  
  
 此示例将创建一个测试数据库和一个登录帐户 `TestLogin1`。 `TestLogin1` 将在该数据库中创建一个 XML 架构集合。 然后，此登录帐户将创建一个表并使用 XML 架构集合创建一个类型化的 xml 列。 用户随后将插入数据并查询该数据。 所有这些步骤都需要必要的架构权限，如代码中所示。  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Create a table by using the collection to type an XML column.   
--TestLogin1 must have permission to create a table.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also must have REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- Now user can create a table and use the XML schema collection to create   
-- a typed XML column.  
SETUSER 'TestLogin1'  
GO  
CREATE TABLE MyTestTable (xmlCol xml (dbo.myTestSchemaCollection))  
GO  
-- To insert data in the table, the user needs EXECUTE permission on the XML schema collection.  
-- GRANT EXECUTE permission to TestLogin2 on the xml schema collection.  
SETUSER  
GO  
GRANT EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- TestLogin1 does not own the dbo schema. This user must have INSERT permission.  
GRANT INSERT TO TestLogin1  
GO  
-- Now the user can insert data into the table.  
SETUSER 'TestLogin1'  
GO  
INSERT INTO MyTestTable VALUES('  
<telephone xmlns="http://schemas.adventure-works.com/Additional/ContactInfo">111-1111</telephone>  
')  
GO  
-- To query the table, TestLogin1 must have permissions: SELECT on the table and EXECUTE on the XML schema collection.  
SETUSER  
GO  
GRANT SELECT TO TestLogin1  
GO  
-- TestLogin1 already has EXECUTE permission on the schema (granted before inserting a record in the table).  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- To show that the user must have EXECUTE permission to query, revoke the  
-- previously granted permission and return the query.  
SETUSER  
GO  
REVOKE EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection to TestLogin1  
Go  
-- Now TestLogin1 cannot execute the query.  
SETUSER 'TestLogin1'  
GO  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="c-granting-alter-permission-on-an-xml-schema-collection"></a>C. 授予对 XML 架构集合的 ALTER 权限  
 要修改数据库中的现有 XML 架构集合，用户必须具有 ALTER 权限。 下面的示例显示如何授予 `ALTER` 权限。  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant ALTER permission to TestLogin1.  
setuser  
GO  
GRANT ALTER ON XML SCHEMA COLLECTION::myTestSchemaCollection TO TestLogin1  
GO  
-- TestLogin1 should be able to add components to the collection.  
SETUSER 'TestLogin1'  
GO  
ALTER XML SCHEMA COLLECTION myTestSchemaCollection ADD '  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns="http://schemas.adventure-works.com/Additional/ContactInfo"   
elementFormDefault="qualified">  
 <xsd:element name="pager" type="xsd:string"/>  
</xsd:schema>  
'  
Go  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="d-granting-take-ownership-permission-on-an-xml-schema-collection"></a>D. 授予对 XML 架构集合的 TAKE OWNERSHIP 权限  
 下面的示例显示如何将 XML 架构的所有权从一个用户传递到另一个用户。 为了使此示例更加生动，此示例中的用户在不同的默认关系架构中工作。  
  
 此示例将执行下列操作：  
  
-   创建一个带有两个关系架构（ `dbo` 和 `myOtherDBSchema`）的数据库。  
  
-   创建两个用户，即 `TestLogin1` 和 `TestLogin2`。 `TestLogin2` 成为 `myOtherDBSchema` 关系架构的所有者。  
  
-   `TestLogin1` 将在 `dbo` 关系架构中创建一个 XML 架构集合。  
  
-   `TestLogin1` 然后向 `TAKE OWNERSHIP` 授予针对 XML 架构集合的 `TestLogin2`权限。  
  
-   `TestLogin2` 将成为 `myOtherDBSchema`中的 XML 架构集合的所有者，而不用更改 XML 架构集合的关系架构。  
  
```  
CREATE LOGIN TestLogin1 with password='SQLSvrPwd1'  
GO  
CREATE LOGIN TestLogin2 with password='SQLSvrPwd2'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
-- Create users in the database. Note TestLogin2's default schema is  
-- myOtherDBSchema.  
CREATE USER TestLogin1  
GO  
CREATE USER TestLogin2 WITH DEFAULT_SCHEMA=myOtherDBSchema  
GO  
-- TestLogin2 will own myOtherDBSchema relational schema.  
ALTER AUTHORIZATION ON SCHEMA::myOtherDBSchema TO TestLogin2  
GO  
  
-- For TestLogin1 to create XML schema collection, the following  
-- permission is required.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- Now TestLogin1 can create an XML schema collection.  
setuser 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
 <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"   
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
 </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Grant TAKE OWNERSHIP to TestLogin2.  
SETUSER  
GO  
GRANT TAKE OWNERSHIP ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Verify the owner. Note the UserName and Principal_id is null.   
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections   
      JOIN sys.schemas   
      ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- TestLogin2 can take ownership now.  
setuser 'TestLogin2'  
GO  
ALTER AUTHORIZATION ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Note that although TestLogin2 is the owner,the XML schema collection   
-- is still in dbo.  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
      sys.schemas.name as RelSchemaName,*   
FROM sys.xml_schema_collections JOIN sys.schemas   
     ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
  
-- TestLogin2 moves the collection from dbo to myOtherDBSchema relational schema.  
-- TestLogin2 already has all necessary permissions.  
-- 1) TestLogin2 owns the destination relational schema so he can alter it.  
-- 2) TestLogin2 owns the XML schema collection (therefore, has CONTROL permission).  
ALTER SCHEMA myOtherDBSchema  
TRANSFER XML SCHEMA COLLECTION::dbo.myTestSchemaCollection  
GO  
  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections JOIN sys.schemas   
       ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
DROP LOGIN TestLogin2  
go   
```  
  
### <a name="e-granting-view-definition-permission-on-an-xml-schema-collection"></a>E. 授予对 XML 架构集合的 VIEW DEFINITION 权限  
 下面的示例显示如何授予对 XML 架构集合的 VIEW DEFINITION 权限。  
  
```  
SETUSER  
GO  
USE master  
GO  
IF EXISTS( SELECT * FROM sysdatabases WHERE name='permissionsDB' )  
   DROP DATABASE permissionsDB  
GO  
IF EXISTS( SELECT * FROM sys.sql_logins WHERE name='schemaUser' )  
   DROP LOGIN schemaUser  
GO  
CREATE DATABASE permissionsDB  
GO  
CREATE LOGIN schemaUser WITH PASSWORD='Pass#123',DEFAULT_DATABASE=permissionsDB  
GO  
GRANT CONNECT SQL TO schemaUser  
GO  
USE permissionsDB  
GO  
CREATE USER schemaUser WITH DEFAULT_SCHEMA=dbo  
GO  
CREATE XML SCHEMA COLLECTION MySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns"  
xmlns:ns="http://ns">  
  
   <simpleType name="ListOfIntegers">  
      <list itemType="integer"/>  
   </simpleType>  
  
   <element name="root" type="ns:ListOfIntegers"/>  
  
   <element name="gRoot" type="gMonth"/>  
  
</schema>  
'  
GO  
-- schemaUser cannot see the contents of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
  
-- Grant schemaUser VIEW DEFINITION and REFERENCES permissions  
-- on the XML schema collection.  
SETUSER  
GO  
GRANT VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
GRANT REFERENCES ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
-- Now schemaUser can see the content of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
-- Revoke schemaUser VIEW DEFINITION permissions  
-- on the XML schema collection.  
SETUSER  
GO  
REVOKE VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC FROM schemaUser  
GO  
-- Now schemaUser cannot see the contents of   
-- the collection.  
setuser 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 架构集合 (SQL Server)](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
