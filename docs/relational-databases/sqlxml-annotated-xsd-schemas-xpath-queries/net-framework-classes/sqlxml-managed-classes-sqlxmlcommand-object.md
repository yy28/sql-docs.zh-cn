---
title: SqlXmlCommand 对象 （SQLXML 托管类） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 89ab6ca4f8b95f4f78b1f6c8b9e33fbd1a3fa138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816275"
---
# <a name="sqlxml-managed-classes---sqlxmlcommand-object"></a>SQLXML 托管类 - SqlXmlCommand 对象
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  这是 SqlXmlCommand 对象的构造函数：  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 其中，`cnString` 是标识服务器、数据库和登录信息的 ADO 或 OLEDB 连接字符串，例如 `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`。  
  
 在该连接字符串中，`Provider` 必须是 SQLOLEDB，并且 `Data Provider` 不应包括在访问接口字符串中。  
  
 有关工作示例，请参阅[执行 SQL 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
## <a name="methods"></a>方法  
 TheSqlXmlCommand 对象支持多个方法，包括以下方法用来执行命令：  
  
 void executenonquery （)  
 执行该命令，但不返回任何内容。 如果您想要执行非查询命令（即，不返回任何内容的命令），则此方法将很有用。 例如，执行更新记录但不返回任何内容的 updategram 或 DiffGram。  
  
 Stream executestream （)  
 返回一个新的 Stream 对象。 在您希望查询结果在新的流中返回给您时，此方法很有用。 有关工作示例，请参阅[执行 SQL 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 public void ExecuteToStream (Stream outputStream)  
 将查询结果写入到现有流中。 当您具有所需结果 （例如，若要获得查询结果写入到 System.Web.HttpResponse.OutputStream） 追加到流时，此方法很有用。 有关工作示例，请参阅[执行 SQL 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 XmlReader executexmlreader （)  
 返回的 XmlReader 对象。 此方法可用于直接操作 XmlReader 对象中的数据或插入 System.Xml 的链式体系结构。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 文档。 有关工作示例，请参阅[通过使用 ExecuteXMLReader 方法执行 SQL 查询](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)。  
  
 TheSqlXmlCommand 对象还支持这些其他方法：  
  
 SqlXmlParameter createparameter （)  
 创建一个 SqlXmlParameter 对象。 可以设置的值*名称*并*值*此对象的参数。 如果您希望将参数传递到某一命令，则此方法很有用。 有关工作示例，请参阅[执行 SQL 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 void clearparameters （)  
 清除为给定命令对象创建的参数。 如果您想要对同一命令对象执行多个查询，则此方法很有用。  
  
## <a name="properties"></a>属性  
 SqlXmlCommand 对象还支持以下属性：  
  
 ClientSideXml  
 在设置为 True 时，指定要在客户端上发生行集到 XML 的转换，而非在服务器上发生。 在希望将性能负荷移到中间层时，此属性很有用。 该属性还允许您使用 FOR XML 包装现有存储过程，以便获取 XML 输出。  
  
 SchemaPath  
 映射架构的名称以及目录路径（例如 C:\x\y\MySchema.xml）。 此属性用于为 XPath 查询指定映射架构。 指定的路径可以是绝对路径或相对路径。 如果该路径是相对的基路径中指定的基路径用于解析该相对路径。 如果未指定基本路径，则相对路径是相对于当前目录的路径。 有关工作示例，请参阅[在.NET 环境中访问 SQLXML 功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
 XslPath  
 XSL 文件的名称以及目录路径。 指定的路径可以是绝对路径或相对路径。 如果该路径是相对的基路径中指定的基路径用于解析该相对路径。 如果未指定基本路径，则相对路径是相对于当前目录的路径。 有关工作示例，请参阅[应用 XSL 转换&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)。  
  
 基路径  
 基本路径（目录路径）。 此属性可用于解析为一个 XSL 文件 （通过使用 XslPath 属性）、 映射架构文件 （通过使用 SchemaPath 属性） 或在 XML 模板中的外部架构引用指定的相对路径 (通过使用指定**映射架构**属性)。  
  
 OutputEncoding  
 为在执行命令时返回的流指定编码。 此属性用于为返回的流请求特定的编码。 某些常用编码是 UTF-8、ANSI 和 Unicode。 UTF-8 为默认编码。  
  
 命名空间  
 允许执行使用命名空间的 XPath 查询。 有关带命名空间的 XPath 查询的详细信息，请参阅[执行带命名空间的 XPath 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)。 有关工作示例，请参阅[执行 XPath 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)。  
  
 RootTag  
 为命令执行生成的 XML 提供单个根元素。 有效的 XML 文档要求单个根级别标记。 如果执行的命令生成 XML 片段（没有单个顶级元素），则可为返回的 XML 指定一个根元素。 有关工作示例，请参阅[应用 XSL 转换&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)。  
  
 CommandText  
 命令的文本。 此属性用于指定您要执行的命令的文本。 有关工作示例，请参阅[执行 SQL 查询&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)。  
  
 CommandStream  
 命令流。 如果您要根据某一文件（例如 XML 模板）执行命令，则此属性很有用。 当您使用 CommandStream，仅 **"模板"**， **"UpdateGram"** 并 **"DiffGram"CommandType**支持值。 有关工作示例，请参阅[通过使用 CommandStream 属性执行模板文件](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)。  
  
 CommandType  
 标识命令的类型。 此属性用于指定您要执行的命令的类型。 下表中的值确定命令的类型。 有关工作示例，请参阅[在.NET 环境中访问 SQLXML 功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|SqlXmlCommandType.Sql|执行某一 SQL 命令（例如 `SELECT * FROM Employees FOR XML AUTO`）。|  
|SqlXmlCommandType.XPath|执行某一 XPath 命令（例如 `Employees[@EmployeeID=1]`）。|  
|SqlXmlCommandType.Template|执行某一 XML 模板。|  
|SqlXmlCommandType.TemplateFile|执行指定路径上的模板文件。|  
|SqlXmlCommandType.UpdateGram|执行 updategram。|  
|SqlXmlCommandType.Diffgram|执行 DiffGram。|  
  
## <a name="see-also"></a>请参阅  
 [SqlXmlParameter 对象&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [SqlXmlAdapter 对象&#40;SQLXML 托管类&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
