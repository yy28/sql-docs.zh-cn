---
title: "用于 XML 报表数据的元素路径语法 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 121f98cb4b10c480b2f6e215c9432361f963475c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>用于 XML 报表数据的元素路径语法 (SSRS)
  在报表设计器中，可以通过定义元素路径（区分大小写）来指定 XML 数据源中要用于报表的数据。 元素路径指示如何遍历 XML 数据源中的 XML 层次结构节点及其属性。 若要使用默认元素路径，请将数据集查询或 XML **ElementPath** 的 XML **Query** 保留为空。 从 XML 数据源检索数据时，具有文本值的元素节点和元素节点属性将成为结果集中的列。 运行查询时，节点值和属性将成为行数据。 该列在“报表数据”窗格中显示为数据集字段集合。 本主题介绍元素路径语法。  
  
> [!NOTE]  
>  元素路径语法与命名空间无关。 若要在元素路径中使用命名空间，请使用包括[用于 XML 报表数据的 XML 查询语法 (SSRS)](../../reporting-services/report-data/xml-query-syntax-for-xml-report-data-ssrs.md) 中介绍的 XML **ElementPath** 元素的 XML 查询语法。  
  
 下表介绍用于定义元素路径的约定。  
  
|约定|用于|  
|----------------|--------------|  
|**粗体**|必须完全按原样键入的文本。|  
||（垂直条）|分隔语法项。 只能选择其中一项。|  
|`[ ]`（方括号）|可选语法项。 不要键入方括号。|  
|**{ }** （大括号）|分隔语法项的参数。|  
|[**,**...*n*]|指示前面的项可以重复 *n* 次。 各项之间以逗号分隔。|  
  
## <a name="syntax"></a>语法  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>注释  
 下表总结了元素路径字词。 该表中的示例引用示例 XML 文档 Customers.xml，该文档包含于本主题的“示例”部分中。  
  
> [!NOTE]  
>  XML 标记区分大小写。 在元素路径中指定 ElementNode 时，必须完全匹配数据源中的 XML 标记。  
  
|术语|定义|  
|----------|----------------|  
|Element path|定义为了使用 XML 数据源检索数据集的字段数据而要在 XML 文档中遍历的节点序列。|  
|**ElementNode**|XML 文档中的 XML 节点。 节点由标记指定，并与其他节点之间存在层次结构关系。 例如，\<Customers> 是根元素节点。 \<Customer> 是 \<Customers> 的子元素。|  
|**XMLName**|节点的名称。 例如，Customers 节点的名称为 Customers。 **XMLName** 可以使用命名空间标识符作为前缀，以唯一命名每个节点。|  
|**编码**|指示此元素的 **Value** 是编码的 XML，它需要解码并作为此元素的子元素。|  
|**字段列表**|定义要用于检索数据的元素和属性集。<br /><br /> 如果未指定，则所有属性和子元素都将用作字段。 如果指定了空字段列表 (**{}**)，则不使用来自该节点的任何字段。<br /><br /> **FieldList** 不可以同时包含 **Value** 以及 **Element** 或 **ElementNode**。|  
|**字段**|指定作为数据集字段检索的数据。|  
|**Attribute**|**ElementNode**中的“名称/值”对。 例如，在元素节点 \<Customer ID="1"> 中，ID 是属性，并且 @ID(Integer) 将返回“1”表示对应数据字段 ID 中的整数类型。|  
|**值**|元素的值。 **Value** 只能在元素路径的最后一个 **ElementNode** 中使用。 例如，由于 \<Return> 是一个叶节点，因此如果将其包含于元素路径的结尾处，则 Return {@} 的值将为 Chair。|  
|**Element**|命名子元素的值。 例如，Customers {}/Customer {}/LastName 仅检索 LastName 元素的值。|  
|**类型**|用于从此元素创建的字段的可选数据类型。|  
|**NamespacePrefix**|**NamespacePrefix** 在 XML 查询元素中定义。 如果不存在 XML 查询元素，则将忽略 XML **ElementPath** 中的命名空间。 如果存在 XML 查询元素，则 XML **ElementPath** 具有可选属性 **IgnoreNamespaces**。 如果 IgnoreNamespaces 为 **true**，XML **ElementPath** 和 XML 文档中的命名空间将被忽略。 有关详细信息，请参阅[用于 XML 报表数据的 XML 查询语法 (SSRS)](../../reporting-services/report-data/xml-query-syntax-for-xml-report-data-ssrs.md)。|  
  
## <a name="example---no-namespaces"></a>示例 - 无命名空间  
 以下示例使用 XML 文档 Customers.xml。 此表以此 XML 文档作为数据源，在此基础上显示了元素路径语法的示例，以及在定义数据集的查询中使用相应元素路径所得到的结果。  
  
> [!NOTE]  
>  当元素路径为空时，查询将使用默认元素路径：指向叶节点集合的第一个路径。 在第一个示例中，将元素路径保留为空等效于指定元素路径 /Customers/Customer/Orders/Order。 将在结果集中返回沿该路径分布的所有节点值和属性，并且节点名和属性名将显示为数据集字段。  
  
 **示例 #1**： *空*  
  
|订单|Qty|ID|FirstName|LastName|Customer.ID|xmlns|  
|-----------|---------|--------|---------------|--------------|-----------------|-----------|  
|Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
|表|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
|Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
|EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
 **示例 #2**： `Customers {}/Customer`  
  
|FirstName|LastName|ID|  
|---------------|--------------|--------|  
|Bobby|Moore|11|  
|Crystal|Hu|20|  
|Wyatt|Diaz|33|  
  
 **示例 #3**： `Customers {}/Customer {}/LastName`  
  
|LastName|  
|--------------|  
|Moore|  
|Hu|  
|Diaz|  
  
 **示例 #4**： `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
|订单|Qty|  
|-----------|---------|  
|Chair|6|  
|表|1|  
|Sofa|2|  
|EndTables|2|  
  
 **示例 #5**： `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
|Order.ID|FirstName|LastName|ID|  
|--------------|---------------|--------------|--------|  
|1|Bobby|Moore|11|  
|2|Bobby|Moore|11|  
|8|Crystal|Hu|20|  
|15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>XML 文档：Customers.xml  
 若要尝试前一节中的元素路径示例，可以复制此 XML 并将其保存到报表设计器可以访问的 URL，然后将该 XML 文档用作 XML 数据源：例如， `http://localhost/Customers.xml`。  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 还可以使用下列步骤，创建不包含连接字符串的 XML 数据源，并在查询中嵌入 Customers.XML：  
  
###### <a name="to-embed-customersxml-in-a-query"></a>在查询中嵌入 Customers.XML  
  
1.  使用空连接字符串创建一个 XML 数据源。  
  
2.  为 XML 数据源创建新的数据集。  
  
3.  在 **“数据集属性”** 对话框中，单击 **“查询设计器”**。 基于文本的查询设计器对话框打开。  
  
4.  在查询窗格中，输入以下两行：  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  复制 Customers.XML 并将文本粘贴到 `<XmlData>`之后的查询窗格中。  
  
6.  在查询窗格中，删除从 Customers.XML 中复制的第一行： `<?xml version="1.0"?>`  
  
7.  在查询的结尾添加以下两行：  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  单击“运行查询(!)”。  
  
     结果集的以下列中显示 4 行数据： `xmlns`、 `Customer.ID`、 `FirstName`、 `LastName`、 `ID`、 `Qty`、 `Order`。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [XML 连接类型 (SSRS)](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Reporting Services 教程 (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
