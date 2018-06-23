---
title: 用于 XML 报表数据的 XML 查询语法 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
caps.latest.revision: 46
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c23e5ef8859f3d0cdf1d0a88dc4bf98b883c64d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129830"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>用于 XML 报表数据的 XML 查询语法 (SSRS)
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，可以为 XML 数据源创建数据集。 定义数据源后，可以为数据集创建查询。 通过包括 XML 根据 XML 数据的数据源指向的类型，创建数据集查询`Query`或元素路径。 XML`Query`开头**\<查询 >** 标记并包括命名空间和数据源而异的 XML 元素。 元素路径与命名空间无关，它使用与 XPath 类似的语法指定要使用的来自基础 XML 数据的节点和节点属性。 有关元素路径的详细信息，请参阅[用于 XML 报表数据的元素路径语法 (SSRS)](report-data-ssrs.md)。  
  
 可以为以下类型的 XML 数据创建 XML 数据源：  
  
-   URL 使用 http 协议指向的 Xml 文档  
  
-   返回 XML 数据的 Web 服务端点  
  
-   嵌入的 XML 数据  
  
 指定 XML `Query` 或元素路径的方式取决于 XML 数据的类型。  
  
 对于 XML 文档，XML`Query`是可选的。 如果包括它，则它可以包含可选的 XML `ElementPath`。 XML `ElementPath` 的值使用元素路径语法。 您可以包含 XML`Query`和 XML`ElementPath`以便正确处理命名空间，需要从数据源的 XML 数据时。  
  
 对于连接字符串 URL 指向的 Web 服务端点，XML `Query` 定义 Web 服务方法和/或 SOAP 操作。 XML 数据提供程序将创建 Web 服务请求，以检索要用于报表的 XML 数据。  
  
> [!NOTE]  
>  当 Web 服务命名空间包括正斜杠 (`/)` 字符时，应同时包括 Web 服务方法和 SOAP 操作，以使 XML 数据处理扩展插件可以正确派生命名空间。  
  
 对于嵌入的 XML 文档，XML`Query`定义要使用的嵌入的 XML 数据、 包括可选命名空间，并包含可选的 XML `ElementPath`...  
  
## <a name="specifying-query-parameters-for-xml-data"></a>指定 XML 数据的查询参数  
 可以为 XML 文档指定查询参数。  
  
-   对于 URL 请求，查询参数以标准 URL 参数的形式包含在查询中。  
  
-   对于 Web 服务请求，需要将查询参数传递给 Web 服务方法。 若要定义查询参数，请使用 **“数据集属性”** 对话框的 **“参数”** 页。 有关详细信息，请参阅[数据集属性对话框中，参数](dataset-properties-dialog-box-parameters.md)。  
  
### <a name="example"></a>示例  
 下表中的示例说明如何从报表服务器 Web 服务、XML 文档和嵌入的 XML 数据中检索数据。  
  
|XML 数据源|查询示例|  
|---------------------|-------------------|  
|ListChildren 方法从 web 服务 XML 数据。|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="http://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|使用 SoapAction 获得的 Web 服务 XML 数据。|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>http://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|使用命名空间的 XML 文档或嵌入的 XML 数据。<br /><br /> 为元素路径指定命名空间的查询元素。|`<Query xmlns:es="http://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|嵌入的 XML 文档。|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|使用默认值的 XML 文档。|*No query*。<br /><br /> 元素路径是从 XML 文档本身派生而来的，并且与命名空间无关。|  
  
> [!NOTE]  
>  第一个 Web 服务示例列出了使用 <xref:ReportService2006.ReportingService2006.ListChildren%2A> 方法获得的 Web 服务 XML 数据。 若要运行此查询，必须创建新的数据源并将连接字符串设置为 http://localhost/reportserver/reportservice2006.asmx。 <xref:ReportService2006.ReportingService2006.ListChildren%2A>方法采用两个参数：`Item`和`Recursive`。 设置的默认值为`Item`到`/`和`Recursive`到`1`。  
  
## <a name="specifying-namespaces"></a>指定命名空间  
 使用 XML`Query`元素，用于从数据源的 XML 数据中指定的命名空间的使用。 下面的 XML 查询使用命名空间 `sales`。 `sales:LineItems` 和 `sales:LineItem` 的 XML `ElementPath` 节点使用命名空间 `sales`。  
  
```  
<Query xmlns:sales=  
"http://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      http://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 若要指定数据提供程序命名空间，以便默认命名空间保留为空，使用`xmldp`。 下面的示例说明了这一点。  
  
### <a name="example"></a>示例  
 以下示例使用 XML 文档 DPNamespace.xml，该表之后提供了该文档以进行说明。 此表显示了包括命名空间前缀的 XML ElementPath 语法的两个示例。  
  
|XML 查询元素|数据集中的结果字段|  
|-----------------------|-------------------------------------|  
|\<Query/>|值答： http://schemas.microsoft.com/..。<br /><br /> 值 b: http://schemas.microsoft.com/..。<br /><br /> 值 c: http://schemas.microsoft.com/..。|  
|\<xmldp:Query xmlns:xmldp ="http://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery"xmlns:ns ="http://schemas.microsoft.com/..。"><br /><br /> \<xmldp:ElementPath > 根{}/ns:Element2 / 节点\</xmldp:ElementPath ><br /><br /> \</xmldp:Query >|值 D<br /><br /> 值 E<br /><br /> 值 F|  
  
#### <a name="xml-document-dpnamespacexml"></a>XML 文档：DPNamespace.xml  
 可以复制此 XML 并将其保存到报表设计器可访问的 URL 以用作 XML 数据源：例如 http://localhost/DPNamespace.xml。  
  
```  
<Root xmlns:ns="http://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 连接类型 (SSRS)](xml-connection-type-ssrs.md)   
 [Reporting Services 教程 (SSRS)](../reporting-services-tutorials-ssrs.md)  
  
  