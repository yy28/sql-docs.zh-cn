---
title: 客户端 XML 格式化 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- middle tier XML formatting [SQLXML]
- client-side XML formatting
- client-side-xml attribute
ms.assetid: 9630a21d-a93b-4d3b-8a25-c4b32399f993
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 95ed0b26f885474b87b45addd08dfcdb67b4bff9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503724"
---
# <a name="client-side-xml-formatting-sqlxml-40"></a>客户端 XML 格式化 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主题提供了有关客户端 XML 格式化的信息。 客户端格式化是指对中间层上的 XML 的格式化。  
  
> [!NOTE]  
>  本主题提供了有关使用客户端上的 FOR XML 子句的其他信息，并假定您已熟悉 FOR XML 子句。 有关 FOR XML 的详细信息，请参阅[使用 FOR XML 构造 XML](../../../relational-databases/xml/for-xml-sql-server.md)。  
  
 **重要**若要将客户端 FOR XML 功能与新**xml**数据类型，应始终使用客户端[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (SQLNCLI11) 数据访问接口而不是 SQLOLEDB 访问接口。 SQLNCLI11 为 SQL Server 访问接口的最新版本，且完全识别 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的数据类型。 FOR XML 与 SQLOLEDB 访问接口会将客户端的行为**xml**以字符串形式的数据类型。  
  
## <a name="formatting-xml-documents-on-the-client-side"></a>对客户端上的 XML 文档进行格式化  
 当客户端应用程序执行以下查询时：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML RAW  
```  
  
 ...仅此部分的查询发送到服务器：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 在服务器执行查询并返回到客户端的行集 （其中包含 FirstName 和 LastNamecolumns）。 然后，中间层对行集应用 FOR XML 转换，并将 XML 格式返回到客户端。  
  
 同样，在您执行 XPath 查询时，服务器将行集返回到客户端，并对客户端上的行集应用 FOR XML EXPLICIT 转换，从而生成所需的 XML 格式。  
  
 下表显示了可以使用客户端 FOR XML 指定的模式。  
  
|客户端 FOR XML 模式|注释|  
|-------------------------------|-------------|  
|RAW|在客户端或服务器端 FOR XML 中指定时产生相同的结果。|  
|NESTED|与服务器端上的 FOR XML AUTO 模式类似。|  
|EXPLICIT|与服务器端 FOR XML EXPLICIT 模式类似。|  
  
> [!NOTE]  
>  如果指定 AUTO 模式并请求客户端 XML 格式化，则整个查询将发送到服务器；即在服务器上进行 XML 格式化。 为了方便起见，执行此操作，但请注意，NESTED 模式会返回基表名称作为生成的 XML 文档中的元素名称。 编写的某些应用程序可能需要基表名称。 例如，您可能会执行存储过程并在数据集中加载生成的数据（[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中），然后生成 DiffGram 以更新表中的数据。 在这种情况下，您需要基表信息且必须使用 NESTED 模式。  
  
## <a name="benefits-of-client-side-xml-formatting"></a>客户端 XML 格式化的优点  
 以下是在客户端上进行 XML 格式化的一些优点。  
  
### <a name="if-you-have-stored-procedures-on-the-server-that-return-a-single-rowset-you-can-request-client-side-for-xml-transformation-to-generate-an-xml"></a>如果您在服务器上具有可返回单个行集的存储过程，则可请求客户端 FOR XML 转换以生成 XML。  
 例如，请考虑以下存储过程。 此过程将返回 AdventureWorks 数据库的 Person.Contact 表中的雇员名字和姓氏：  
  
```  
IF EXISTS (SELECT name FROM sysobjects  
   WHERE name = 'GetContacts' AND type = 'P')  
   DROP PROCEDURE GetContacts  
GO  
CREATE PROCEDURE GetContacts  
AS  
    SELECT   FirstName, LastName  
    FROM     Person.Contact  
```  
  
 以下 XML 模板示例将执行此存储过程。 FOR XML 子句在存储过程名称之后指定。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    EXEC GetContacts FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 因为**客户端侧 xml**属性设置为 1 (true) 在模板中，在服务器上执行存储的过程和中间层上转换为 XML 并返回到服务器返回的两列行集客户端。 （此处仅显示部分结果。）  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact FirstName="Catherine" LastName="Abel" />  
</ROOT>  
```  
  
> [!NOTE]  
>  当使用 sqlxmloledb 访问接口或 SQLXML 托管类时，可以使用**ClientSideXml**属性来请求客户端 XML 格式。  
  
### <a name="the-workload-is-more-balanced"></a>工作负荷更加均衡。  
 由于客户端进行 XML 格式化，因此会在服务器与客户端之间均衡工作负荷，从而释放服务器执行其他操作。  
  
## <a name="supporting-client-side-xml-formatting"></a>支持客户端 XML 格式化  
 为了支持客户端 XML 格式化功能，SQLXML 提供：  
  
-   SQLXMLOLEDB 访问接口  
  
-   SQLXML 托管类  
  
-   增强的 XML 模板支持  
  
-   SqlXmlCommand.ClientSideXml 属性  
  
     通过将 SQLXML 托管类的此属性设置为 True，可指定客户端格式。  
  
## <a name="enhanced-xml-template-support"></a>增强的 XML 模板支持  
 开头[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]中的 XML 模板[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]已得到增强的加法**客户端侧 xml**属性。 如果此属性设置为 True，将在客户端上进行 XML 格式化。 请注意，此模板特性在功能上与特定于 SQLXMLOLEDB 提供程序的 ClientSideXML 属性相同。  
  
> [!NOTE]  
>  如果正在使用 sqlxmloledb 访问接口的 ADO 应用程序中执行 XML 模板，并且同时指定**客户端侧 xml**模板和提供程序 ClientSideXML 属性中指定的值中的属性模板将优先。  
  
## <a name="see-also"></a>请参阅  
 [客户端和服务器端 XML 格式的体系结构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)   
 [FOR XML 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [xml 在 SQLXML 4.0 中的数据类型支持](../../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)   
 [SQLXML 托管类](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)   
 [客户端与服务器端 XML 格式设置&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-vs-server-side-xml-formatting-sqlxml-4-0.md)   
 [SqlXmlCommand 对象&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [XML 数据 (SQL Server)](../../../relational-databases/xml/xml-data-sql-server.md)  
  
  
