---
title: 撤消对 XML 架构集合的权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 547ae02c8041dcdd1b7eced9a3a4cf5402834572
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166997"
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>撤消对 XML 架构集合的权限
  可以使用下列一种方法撤消创建 XML 架构集合的权限：  
  
-   撤消对关系架构的 ALTER 权限。 这样，主体就不能在关系架构中创建 XML 架构集合。 但是，主体仍然可以在同一数据库的其他关系架构中执行此操作。  
  
-   撤消主体对数据库的 ALTER ANY SCHEMA 权限。 这样，主体就不能在数据库中的任何位置创建 XML 架构集合。  
  
-   撤消主体对数据库的 CREATE XML SCHEMA COLLECTION 或 ALTER XML SCHEMA COLLECTION 权限。 这样，主体就无法在数据库中导入 XML 架构集合。 撤消对数据库的 ALTER 或 CONTROL 权限效果相同。  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>撤消对现有 XML 架构集合对象的权限  
 下列是可以对 XML 架构集合撤消的权限及相应结果：  
  
-   ALTER 权限，撤消后，主体无法修改 XML 架构集合的内容。  
  
-   TAKE OWNERSHIP 权限，撤消后，主体无法传输 XML 架构集合的所有权。  
  
-   REFERENCES 权限，撤消后，主体无法使用 XML 架构集合类型化或约束 xml 类型列（表和视图中）和参数。 它还撤消了从其他 XML 架构集合中引用此架构集合的权限。  
  
-   VIEW DEFINITION 权限，撤消后，主体无法查看 XML 架构集合的内容。  
  
-   EXECUTE 权限，撤消后，主体无法在通过 XML 集合类型化或约束的列、变量和参数中插入或更新值。 它还撤消了查询这类 **xml** 类型列、变量或参数的功能。  
  
## <a name="examples"></a>示例  
 以下示例中的应用场景说明 XML 架构权限的工作机制。 每个示例都创建有必需的测试数据库、关系架构和登录帐户。 这些登录帐户已授予必需的 XML 架构集合权限。 每个示例在结束时都会进行必要的清除操作。  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>A. 撤消创建 XML 架构集合的权限  
 该示例创建了一个登录帐户和一个示例数据库。 并在数据库中添加了一个关系架构。 首先，为登录帐户授予对两个关系架构的 ALTER 权限和其他所需权限，以创建 XML 架构集合。 然后，该示例撤消了对数据库中一个关系架构的 ALTER 权限。 这使得登录帐户无法创建 XML 架构集合。  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 数据 (SQL Server)](xml-data-sql-server.md)   
 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)   
 [XML 架构集合 (SQL Server)](xml-schema-collections-sql-server.md)   
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
