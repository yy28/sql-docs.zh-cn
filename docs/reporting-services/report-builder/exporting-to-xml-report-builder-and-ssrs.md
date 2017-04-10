---
title: "导出到 XML（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# 导出到 XML（报表生成器和 SSRS）
  XML 呈现扩展插件可以按 XML 格式返回分页报表。 报表 XML 的架构专用于相应的报表，并且只包含数据。 布局信息呈现以及分页都不是由 XML 呈现扩展插件完成。 此扩展插件生成的 XML 可以导入到数据库中用作 XML 数据消息，或发送到自定义应用程序。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> 报表项  
 下表对各报表项的呈现形式进行了说明：  
  
|项|呈现行为|  
|----------|------------------------|  
|报告|呈现为 XML 文档的顶级元素。|  
|数据区域|呈现为其容器的元素中的某个元素。 数据区域包括表、矩阵和列表，它们将数据显示为文本和图表、数据条、迷你图、仪表以及形象地展现数据的指示器。|  
|组和详细信息部分|每个实例呈现为其容器的元素中的某个元素。|  
|文本框|呈现为其容器中的某个属性或元素。|  
|Rectangle|呈现为其容器中的某个元素。|  
|矩阵列组|呈现为行组中的元素。|  
|映射|呈现为其容器的元素中的某个元素。 地图层是地图的子元素，每个地图层包括其地图成员和地图成员属性的元素。|  
|图表|呈现为其容器的元素中的某个元素。 序列是图表的子元素，而类别是序列的子元素。 为每个图表值呈现所有图表标签。 标签和值作为属性包括。|  
|数据条|呈现为其容器的元素中的某个元素，与图表相似。 通常，数据条并不包括层次结构或标签，而只包含值。|  
|迷你图|呈现为其容器的元素中的某个元素，与图表相似。 通常，迷你图并不包括层次结构或标签，而只包含值。|  
|测量|呈现为其容器的元素中的某个元素。 作为单个元素呈现，它以刻度的最小值和最大值、范围的起始和终止值以及指针的值作为属性。|  
|指示器|呈现为其容器的元素中的某个元素，与仪表相似。 作为单个元素呈现，它以活动状态名称、可用状态以及数据值作为属性。|  
  
 使用 XML 呈现扩展插件呈现报表时，同样遵偱以下规则：  
  
-   XML 元素和属性以其在报表定义中出现的顺序呈现。  
  
-   将忽略分页。  
  
-   不会呈现页眉和页脚。  
  
-   不会呈现无法切换为可见状态的隐藏项。 最初可见的项以及能够切换为可见状态的隐藏项都可以呈现。  
  
-   将忽略**Images, lines, and custom report items** 。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="DataTypes"></a> 数据类型  
 为文本框元素或属性分配的 XSD 数据类型将基于文本框显示的值。  
  
|如果所有文本框值都是|分配的数据类型为|  
|--------------------------------|---------------------------|  
|**Int16**、 **Int32**、 **Int64**、 **UInt16**、 **UInt32**、 **UInt64**、 **Byte**、 **SByte**|**xsd:integer**|  
|**Decimal**（或 **Decimal** 和任何整数或字节数据类型）|**xsd:decimal**|  
|**Float**（或 **Decimal** 和任何整数或字节数据类型）|**xsd:float**|  
|**Double**（或 **Decimal** 和任何整数或字节数据类型）|**xsd:double**|  
|**DateTime 或 DateTime Offset**|**xsd:dateTime**|  
|**Time**|**xsd:string**|  
|**Boolean**|**xsd:boolean**|  
|**String**、 **Char**|**xsd:string**|  
|其他|**xsd:string**|  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="XMLSpecificRenderingRules"></a> 特定于 XML 的呈现规则  
 下面一节将说明 XML 呈现扩展插件是如何解释报表内的报表项的。  
  
### 表体  
 报表将呈现为 XML 文档的根元素。 该元素的名称来自“属性”窗格中设置的 DataElementName 属性。  
  
 在该报表元素中还将包含 XML 命名空间定义和架构引用属性。 变量将以粗体形式注明：  
  
 \<**Report** xmlns=”**SchemaName**” xmlns:xsi=”http://www.w3.org/2001/XMLSchema-instance” xsi:**schemaLocation**=”**SchemaNameReportURL**&amp;rc%3aSchema=true” Name=”ReportName”>  
  
 变量的值如下所示：  
  
|名称|“值”|  
|----------|-----------|  
|报表|Report.DataElementName|  
|ReportURL|服务器上该报表的 URL 编码形式的绝对 URL。|  
|SchemaName|Report.SchemaName。 如果为 Null，则为 Report.Name。 如果使用了 Report.Name，则将首先使用 XmlConvert.EncodeLocalName 对其进行编码。|  
|ReportName|报表的名称。|  
  
### 文本框  
 根据 DataElementStyle RDL 属性，文本框将呈现为元素或特性。 元素或特性的名称来自 TextBox.DataElementName RDL 属性。  
  
### 图表、数据条和迷你图  
 图表、数据条和迷你图使用 XML 来呈现。 其数据是结构化数据。  
  
### 仪表和指示器  
 仪表和指示器使用 XML 来呈现。 其数据是结构化数据。  
  
### 子报表  
 子报表呈现为元素。 元素的名称来自 DataElementName RDL 属性。 报表的 TextBoxesAsElements 属性设置将覆盖子报表中该属性的设置。 命名空间和 XSLT 属性不会添加到子报表元素中。  
  
### 矩形  
 矩形呈现为一个元素。 元素的名称来自 DataElementName RDL 属性。  
  
### 自定义报表项  
 CustomReportItems (CRI) 对于呈现扩展插件来说不可见。 如果报表中存在自定义报表项，则呈现扩展插件将把该自定义报表项呈现为常规报表项。  
  
### 映像  
 不会呈现图像。  
  
### 线条  
 不会呈现线条。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
### 表、矩阵和列表  
 表、矩阵和列表将呈现为元素。 元素的名称来自 Tablix DataElementName RDL 属性。  
  
#### 行和列  
 列在行内呈现。  
  
#### Tablix 角  
 不会呈现角。 只有角的内容才会呈现。  
  
#### Tablix 单元  
 Tablix 单元呈现为元素。 元素的名称来自该单元的 DataElementName RDL 属性。  
  
#### 自动小计  
 不会呈现 Tablix 自动小计。  
  
#### 组内不重复的行项和列项  
 组内不重复的项（例如标签、小计和总计）将呈现为元素。 元素的名称来自 TablixMember.DataElementName RDL 属性。  
  
 TablixMember.DataElementOutput RDL 属性控制是否呈现非重复项。  
  
 如果未提供 Tablix 成员的 DataElementName 属性，将以如下格式动态生成非重复项的名称：  
  
 RowX – 对于非重复行而言，其中 X 是当前父级范围内从零开始的行索引。  
  
 ColumnY – 对于非重复列而言，其中 Y 是当前父级范围内从零开始的列索引。  
  
 非重复表头将呈现为组内不重复的行或列的子级。  
  
 如果非重复成员没有对应的 Tablix 单元，则不会呈现该成员。 如果 Tablix 单元跨越多个列，则可能会出现这种情况。  
  
#### 组内重复的行和列  
 组内重复的行和列将按照 Tablix.DataElementOutput 规则呈现。 元素的名称来自 DataElementName 属性。  
  
 组内的每个唯一值将呈现为该组的子元素。 元素的名称来自 Group.DataElementName 属性。  
  
 如果 DataElementOutput 属性的值等于 Output，则重复项的表头将呈现为详细信息元素的子级。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="CustomFormatsXSLTransformations"></a> 自定义格式和 XSL 转换  
 使用 XSL 转换 (XSLT) 可以将 XML 呈现扩展插件生成的 XML 文件转换为几乎任意格式的文件。 您可以使用此功能来生成现有呈现扩展插件尚不支持的格式的数据。 在尝试创建自己的呈现扩展插件之前，请首先考虑使用 XML 呈现扩展插件和 XSLT。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="DuplicateName"></a> 名称重复  
 如果在同一范围内存在重复的数据元素名称，呈现器将显示一个错误消息。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="XSLTTransformations"></a> XSLT 转换  
 XML 呈现器可将服务器端 XSLT 转换应用到原始 XML 数据。 应用 XSLT 后，呈现器将输出转换后的内容而不是原始 XML 数据。 转换是在服务器而不是客户端上进行的。  
  
 应用到输出的 XSLT 可通过报表的 DataTransform 属性在报表定义文件中定义，或者使用 XSLT *DeviceInfo* 参数进行定义。 如果设置了以上值中的任意一个值，则每次使用 XML 呈现器时都会发生转换。 当使用订阅时，则必须在 RDL DataTransform 属性中定义 XSLT。  
  
 如果同时使用了 DataTransform 定义属性和设备信息设置来指定 XSLT 文件，则会先执行在 DataTransform 中指定的 XSLT 转换，然后执行由设备信息设置指定的 XSLT 转换。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
###  <a name="DeviceInfo"></a> 设备信息设置  
 您可以通过更改如下设备信息设置来更改此呈现器的某些默认设置：  
  
-   应用于 XML 的转换 (XSLT)。  
  
-   XML 文档的 MIME 类型。  
  
-   是否将格式字符串应用于数据。  
  
-   是否缩进 XML 输出。  
  
-   是否包含 XML 架构名称。  
  
-   XML 文档的编码。  
  
-   XML 文档的文件扩展名。  
  
 有关详细信息，请参阅 [XML Device Information Settings](../../reporting-services/xml-device-information-settings.md)。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [返回页首](#BackToTop)  
  
## 另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive functionality - different report rendering extensions.md)   
 [呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  