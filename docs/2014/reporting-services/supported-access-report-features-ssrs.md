---
title: 支持的 Access 报表功能 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0d3c218b5e72e231179443c146a6ea3c23747d4e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180607"
---
# <a name="supported-access-report-features-ssrs"></a>支持的 Access 报表功能 (SSRS)
  将报表导入报表设计器时，导入过程会将 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 报表转换为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表定义语言 (RDL) 文件。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持多项 Access 功能；但是，由于 Access 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 之间存在差异，因此某些功能会略有修改或不受支持。 本主题介绍如何将 Access 报表功能转换为 RDL。  
  
## <a name="importing-access-reports"></a>导入 Access 报表  
 某些查询包含专用于 Access 的代码。 Access 代码不随报表导入。 另外，如果查询包含嵌入的字符串，则相应的报表可能无法正确导入。 若要解决此问题，请使用字符代码来替代这些字符串。 例如，使用 CHAR(34) 来替代逗号 (,) 字符。  
  
 导入过程不能正确地传递分号 （;） 或 XML 标记字符 (\<，> 等) 中的连接字符串信息。 如果连接字符串包含分号或 XML 标记字符，则在导入报表后，必须手动设置新报表中的密码。  
  
 导入过程不会导入连接字符串中的连接设置或常规超时设置。 导入报表后，您可能必须调整这些设置。  
  
 如果所导入的报表包含带有查询参数的查询，则在导入报表时将不转换查询。 若要将查询与报表一同导入，请暂时先用硬编码值替换 Access 报表中的查询参数，然后在导入报表后再用查询参数来替换这些值。  
  
## <a name="page-layout"></a>页面布局  
 Access 中的页面布局与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的页面布局不同。 Access 使用“带区”在页上排列报表项，所谓“带区”是指页上垂直排列的区域。 这些区域可以包含报表表头、报表表尾、页眉、页脚、组和详细信息。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的布局则更为灵活。 数据区域提供了分组功能和详细信息，而且您可以将多个数据区域放在表体中的任何位置，甚至可以并列放置多个数据区域。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 还带有“带状”的页眉和页脚，这一点类似于 Access 中的页眉和页脚。  
  
 将报表从 Access 导入到报表设计器时，Access 报表的页眉和页脚将转换为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表的页眉和页脚。 组和详细信息将转换到列表数据区域中。 报表表头和表尾将置于表体中，而不是位于单独的带区中。 这可能会导致项的位置与其在 Access 报表中的位置稍有不同。  
  
> [!NOTE]  
>  在某些 Access 报表中，相邻的两个报表项可能会重叠。 使用报表设计器导入报表时，不会更正这种重叠情况，并且可能导致运行报表时出现意外结果。  
  
## <a name="data-sources"></a>“数据源”  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持 OLE DB 数据源，例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如果您是从 Access 项目 (.adp) 文件导入报表，则数据源的连接字符串将从 .adp 文件的连接字符串中获取。 如果您是从 Access 数据库（.mdb 或 .accdb）文件导入报表，则连接字符串可能会指向 Access 数据库，并且您在导入报表后可能需要更正该字符串。 如果 Access 报表的数据源是一个查询，则无需在 RDL 中进行修改即可存储此查询信息。 如果 Access 报表的数据源是一个表，则转换过程将根据表名和该表中的字段创建一个查询。  
  
## <a name="reports-with-custom-modules"></a>带有自定义模块的报表  
 如果没有自定义[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vbprvb](../includes/vbprvb-md.md)]代码包含在模块，它不会转换。 如果报表设计器导入过程中遇到代码，生成并显示在一条警告**任务列表**窗口。  
  
## <a name="report-controls"></a>报表控件  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持下列 Access 控件，并在转换后的报表定义中包含这些控件。  
  
|||||  
|-|-|-|-|  
|图像|标签|行|Rectangle|  
|SubForm|SubReport<br /><br /> **请注意**虽然 SubReport 控件主报表中的转换，但子报表本身将单独转换。|TextBox||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下控件：  
  
|||||  
|-|-|-|-|  
|BoundObjectFrame|CheckBox|ComboBox|CommandButton|  
|CustomControl|ListBox|ObjectFrame|OptionButton|  
|TabControl|ToggleButton|||  
  
 如果报表设计器在导入过程中遇到上述任何一个控件，生成并显示在一条警告**任务列表**窗口。  
  
 诸如 ActiveX 和 Office Web 组件等之类的其他控件将不导入。 例如，如果 Access 报表包含 OWC 图表控件，则在导入报表时将不对其进行转换。  
  
## <a name="report-properties"></a>报表属性  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下可通过 Access 用户界面使用的属性。 不支持只能在代码中使用的属性，并且也不在此列出。  
  
|||||  
|-|-|-|-|  
|BackColor|BackStyle|BorderColor|BorderStyle|  
|BorderWidth|BottomMargin|CanGrow（文本框）|CanShrink（文本框）|  
|Caption|FontBold|FontItalic|FontName|  
|FontSize|FontUnderline|FontWeight|ForceNewPage|  
|ForeColor|高度|HideDuplicates|超链接|  
|IsHyperlink|IsVisible|KeepTogether（组）|Left|  
|LeftMargin|LineSlant|LineSpacing|LinkChildFields|  
|LinkMasterFields|NewRowOrCol|PageFooter|PageHeader|  
|页|Picture|PictureTiling（报表）|ReadingOrder|  
|RepeatSection|RightMargin|RunningSum|SizeMode|  
|TextAlign|TOP|TopMargin|宽度|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下可通过 Access 用户界面使用的属性。  
  
|||||  
|-|-|-|-|  
|CanGrow（区域）|CanShrink（区域）|DecimalPlaces|FastLaserPrinting|  
|“筛选器”|FilterOn|“格式”|FormatConditions|  
|GrpKeepTogether|KeepTogether（区域）|NumeralShapes|Orientation|  
|PaintPalette|PaletteSource|PictureAlignment|PicturePages|  
|PictureSizeMode|PictureTiling（图像）|ScrollBars|SpecialEffect|  
|垂直||||  
  
## <a name="grouping"></a>分组  
 Access 使用以下三种属性的组合来定义组级别：组表达式、`GroupOn` 属性以及 `GroupInterval` 属性。 不含组头或组尾的组将与其所包含的组一起合并。 如果该组不包含其他组，则对详细信息区域进行排序并删除该组。  
  
## <a name="expressions"></a>表达式  
 Access 使用表达式来指定文本框中显示的值。 除了一些聚合函数外，Access 还可将 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 用作其表达式语言。 报表设计器将这些 Access 表达式转换为报表表达式。  
  
### <a name="functions"></a>函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表定义将 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET 用作其本机表达式语言，而 Access 2002 则使用 Visual Basic。 以下列表介绍了 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 所支持的函数。  
  
#### <a name="array-functions"></a>数组函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下数组函数：  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>转换函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下转换函数：  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|Cdate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|“格式”|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下转换函数：  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>数据库函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下数据库函数：  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|分区|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下数据库函数：  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>日期/时间函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下日期/时间函数：  
  
|||||  
|-|-|-|-|  
|date|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|Day|  
|Hour|Minute|Month|MonthName|  
|现在|第二个|Time|Time$|  
|Timer|TimeSerial|TimeValue|Weekday|  
|WeekdayName|Year|||  
  
#### <a name="ddeole-functions"></a>DDE/OLE 函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下 DDE/OLE 函数：  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>域聚合函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下域聚合函数：  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>错误处理函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下错误处理函数：  
  
|||||  
|-|-|-|-|  
|Err|错误|Error$|IsError|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下错误处理函数：  
  
-   CVErr  
  
#### <a name="financial-functions"></a>财务函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下财务函数：  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|Rate|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>交互函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下交互函数：  
  
|||||  
|-|-|-|-|  
|Command|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|Seek|SetAttr|  
|Shell|Spc|Tab||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下交互函数：  
  
|||||  
|-|-|-|-|  
|DoEvents|In|输入|Input$|  
  
#### <a name="inspection-functions"></a>检查函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下检查函数：  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下检查函数：  
  
-   IsMissing  
  
#### <a name="math-functions"></a>数学函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下数学函数：  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|smallint|日志|Rnd|  
|舍入|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>消息函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支持以下消息函数：  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>程序流函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下程序流函数：  
  
|||||  
|-|-|-|-|  
|Choose|IIf|开关||  
  
#### <a name="sql-aggregate-functions"></a>SQL 聚合函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下 SQL 聚合函数：  
  
|||||  
|-|-|-|-|  
|Avg|Count|Max|Min|  
|StDev|StDevP|SUM|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>文本函数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持以下文本函数：  
  
|||||  
|-|-|-|-|  
|“格式”|Format$|InStr|InStrRev|  
|LCase|LCase$|Left|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|替换|Right|Right$|  
|RTrim|Space|Space$|StrComp|  
|StrConv|String|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>常量  
 Access 不支持在表达式中使用特殊的 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 常量（例如 `vbTrue`），因而不必转换。 但是，有一点例外：关键字 `Null` 将转换为 `System.DbNull.Value`。  
  
### <a name="parameters"></a>Parameters  
 在导入过程中，报表设计器会对报表内的每个表达式进行扫描，以找出与字段名或控件不相对应的变量。 这些变量将添加到报表参数中。  
  
 存储过程参数的数据类型始终作为字符串导入。 导入报表后，必须手动更改参数，才可使用正确的数据类型。  
  
### <a name="object-names"></a>对象名称  
 Access 允许字段与控件使用相同的名称；而 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不允许。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0 允许在变量名中使用空格；而 Visual Basic .NET 不允许。 如果存在多个名称相同的对象，则导入过程将会使用有效的名称来替换所有这类对象的名称，并为它们分配唯一的名称。 然后，将对每个表达式进行扫描，并使用新名称来替换与已重命名的对象相对应的变量名。  
  
## <a name="rectangles-and-containment"></a>矩形框和包容  
 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表定义中，矩形框可以包含其他报表项。 任何大于报表项并且其 90% 以上的区域与报表项重叠的矩形框都将成为报表项的容器。  
  
## <a name="bitmaps"></a>位图  
 导入报表后，嵌入在报表中的所有位图都会转换为 .bmp 格式，而不管其最初是何种格式。 例如，如果报表中包含 .jpg 和 .gif 文件，则这些资源与报表一起导入后都将转换为 .bmp 文件。 位图可作为嵌入图像存储在报表中。 有关嵌入图像的信息，请参阅[映像&#40;报表生成器和 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)。  
  
## <a name="other-considerations"></a>其他注意事项  
 除前面几项之外，以下信息也适用于从 Access 导入的报表：  
  
-   不转换条件格式。  
  
-   不转换 Access 的报表属性中的说明字段。  
  
  
