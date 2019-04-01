---
title: 拒绝对 XML 架构集合的权限 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: baa1f607e9bdce0dfedc989125e5d29111d44f93
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511604"
---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>拒绝对 XML 架构集合的权限
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  可以拒绝创建新 XML 架构集合或使用现有 XML 架构集合的权限。  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>拒绝创建 XML 架构集合的权限  
 可以通过下列方式拒绝创建 XML 架构集合的权限：  
  
-   拒绝对关系架构的 ALTER 权限。  
  
-   拒绝对关系架构的 CONTROL 权限可拒绝关系架构及其包含的所有对象的所有权限。  
  
-   拒绝对数据库的 ALTER ANY SCHEMA 权限。 在这种情况下，主体无法在数据库的任意位置创建 XML 架构集合。 请注意，拒绝对数据库的 ALTER 或 CONTROL 权限将拒绝对数据库中所有对象的所有权限。  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>拒绝对 XML 架构集合对象的权限  
 下面是可以拒绝的对现有 XML 架构集合的权限及结果：  
  
-   拒绝 ALTER 权限将拒绝主体修改 XML 架构集合内容的功能。  
  
-   拒绝 CONTROL 权限将拒绝主体对 XML 架构集合执行任何操作的功能。  
  
-   拒绝 REFERENCES 权限将拒绝主体使用 XML 架构集合类型化或约束 xml 类型列和参数的功能。 还将拒绝主体从其他 XML 架构集合引用此 XML 架构集合的功能。  
  
-   拒绝 VIEW DEFINITION 权限将拒绝主体查看 XML 架构集合内容的功能。  
  
-   拒绝 EXECUTE 权限将拒绝主体插入或更新由 XML 架构集合类型化或受其约束的列、变量和参数中的值的功能。 还将拒绝主体查询相同 xml 类型列和变量的值的功能。  
  
## <a name="examples"></a>示例  
 以下示例中的应用场景说明了 XML 架构权限的工作机制。 每个示例都创建有必需的测试数据库、关系架构和登录帐户。 这些登录帐户已授予必需的 XML 架构集合权限。 每个示例在结束时都会进行必要的清除操作。  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>A. 禁止用户创建 XML 架构集合  
 禁止用户创建 XML 架构集合的一个方法是拒绝对关系架构的 ALTER 权限。 下面的示例说明了这一点。  
  
 该示例创建了一个用户 `TestLogin1`和一个数据库。 除 `dbo` 架构外，它还在数据库中创建了一个关系架构。 最初， `CREATE XML SCHEMA` 权限允许用户在数据库的任何位置创建架构集合。 然后，该示例拒绝用户对其中一个关系架构拥有 `ALTER` 权限。 这就禁止了用户在该关系架构中创建 XML 架构集合。  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
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
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>B. 拒绝对 XML 架构集合的权限  
 下面的示例说明了如何拒绝登录名对现有 XML 架构集合拥有特定权限。 在本例中，拒绝了测试登录名对现有 XML 架构集合的 REFERENCES 权限。  
  
 该示例创建了一个用户 `TestLogin1`和一个数据库。 除 `dbo` 架构外，它还在数据库中创建了一个关系架构。 最初， `CREATE XML SCHEMA` 权限允许用户在数据库的任何位置创建架构集合。  
  
 `REFERENCES` 利用对 XML 架构集合的 `TestLogin1` 权限使用架构在表中创建 `xml` 类型的列。 如果对 XML 架构集合的 `REFERENCES` 权限被拒绝，将禁止 `TestLogin1` 使用 XML 架构集合。  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
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
  
## <a name="see-also"></a>另请参阅  
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 架构集合 (SQL Server)](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [在服务器上使用 XML 架构集合的要求和限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [DENY 对象权限 (Transact-SQL)](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [GRANT 对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
