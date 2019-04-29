---
title: Foreach 循环编辑器 （集合页） |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.collection.f1
ms.assetid: 95a19dde-61ca-4d9b-aa3d-131fa4264296
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c855cdfbcf622465390e433312d75343242aee50
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894528"
---
# <a name="foreach-loop-editor-collection-page"></a>Foreach 循环编辑器（“集合”页）
  可以使用“Foreach 循环编辑器”对话框的“集合”页，指定枚举器类型以及配置枚举器。  
  
 若要了解有关 Foreach 循环容器以及如何对其进行配置的信息，请参阅 [Foreach 循环容器](control-flow/foreach-loop-container.md)和[配置 Foreach 循环容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
## <a name="static-options"></a>静态选项  
 **枚举器**  
 从列表中选择枚举器类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Foreach 文件枚举器**|枚举文件。 选择此值将显示 **“Foreach 文件枚举器”** 部分中的动态选项。|  
|**Foreach 项枚举器**|枚举项中的值。 选择此值将显示 **“Foreach Item 枚举器”** 部分中的动态选项。|  
|**Foreach ADO 枚举器**|枚举表或表中的行。 选择此值将显示 **“Foreach ADO 枚举器”** 部分中的动态选项。|  
|**Foreach ADO.NET 架构行集枚举器**|枚举架构。 选择此值将显示 **“Foreach ADO.NET 枚举器”** 部分中的动态选项。|  
|**Foreach 源变量枚举器**|枚举变量中的值。 选择此值将显示 **“Foreach 源变量枚举器”** 部分中的动态选项。|  
|**Foreach Nodelist 枚举器**|枚举 XML 文档中的节点。 选择此值将显示 **“Foreach Nodelist 枚举器”** 部分中的动态选项。|  
|**Foreach SMO 枚举器**|枚举 SMO 对象。 选择此值将显示 **“Foreach SMO 枚举器”** 部分中的动态选项。|  
|**Foreach Azure Blob 枚举器**|枚举指定 blob 位置中的 blob 文件。 选择此值将显示 **“Foreach Azure Blob 枚举器”** 部分中的动态选项。|  
|**Foreach ADLS 文件枚举器**|枚举筛选器与 adls 的文件。 选择此值会显示“Foreach ADLS 文件枚举器”部分中的动态选项。|
  
 **表达式**  
 单击或展开 **表达式** 可以查看现有属性表达式的列表。 单击省略号按钮 (…) 可以添加枚举器属性的属性表达式，或编辑并计算现有属性表达式。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 表达式](expressions/integration-services-ssis-expressions.md)、[属性表达式编辑器](expressions/property-expressions-editor.md)、[表达式生成器](expressions/expression-builder.md)  
  
## <a name="enumerator-dynamic-options"></a>枚举器动态选项  
  
### <a name="enumerator--foreach-file-enumerator"></a>Enumerator = Foreach 文件枚举器  
 您可以使用 Foreach 文件枚举器枚举文件夹中的文件。 例如，如果 Foreach 循环包括执行 SQL 任务，则可以使用 Foreach 文件枚举器枚举包含执行 SQL 任务运行的 SQL 语句的文件。 可以将枚举器配置为包括子文件夹。  
  
 Foreach 文件枚举器枚举的文件夹和子文件夹的内容可能在执行循环时发生更改，因为循环中的外部进程或任务会在执行循环时添加、重命名或删除文件。 这意味着可能会出现许多意外情况：  
  
-   如果删除文件，则 Foreach 循环中的某个任务可能会处理一组与后续任务所用的文件不同的文件。  
  
-   如果重命名文件并且外部进程自动添加文件以替换重命名的文件，则 Foreach 循环可能针对相同的文件内容执行两次操作。  
  
-   如果添加文件，则可能很难确定 Foreach 循环要处理的文件。  
  
 **文件夹**  
 提供要枚举的根文件夹的路径。  
  
 **“浏览”**  
 浏览以定位到根文件夹。  
  
 **“文件”**  
 指定要枚举的文件。  
  
> [!NOTE]  
>  使用通配符 (*) 可以指定要包括在集合中的文件。 例如，要包括名称包含“abc”的文件，请使用下面的筛选器：abc\*\*。  
>   
>  当指定文件扩展名时，枚举器还会返回与所追加的附加字符具有相同扩展名的文件。 （这与操作系统中的 **dir** 命令的行为相同，该命令也会比较 8.3 文件名以检查是否具有向后兼容性。）枚举器的这种行为可能会导致意外的结果。 例如，您只想枚举 Excel 2003 文件且指定了“*.xls”。 但是，枚举器还会返回 Excel 2007 文件，因为这些文件具有扩展名“.xlsx”。  
>   
>  可以通过在“集合”页上展开“表达式”，选择 FileSpec 属性，然后单击省略号按钮 (…) 来添加属性表达式，从而使用表达式指定要在集合中包含的文件。 有关动态选择指定的文件的详细信息，请参阅[SSIS 动态设置文件掩码：FileSpec](https://go.microsoft.com/fwlink/?LinkId=238154)  
  
 **完全限定的**  
 选择此项可以检索文件名的完全限定路径。 如果在“文件”选项中指定通配符，则返回的完全限定路径与该筛选条件匹配。  
  
 **仅名称**  
 选择此项可以只检索文件名。 如果在“文件”选项中指定了通配符，则返回的文件名与该筛选条件匹配。  
  
 **名称和扩展名**  
 选择此项可以检索文件名及其文件扩展名。 如果在“文件”选项中指定通配符，则返回的文件名和文件扩展名与该筛选条件匹配。  
  
 **遍历子文件夹**  
 选择此项可以在枚举中包括子文件夹。  
  
### <a name="enumerator--foreach-item-enumerator"></a>Enumerator = Foreach Item 枚举器  
 您可以使用 Foreach Item 枚举器枚举集合中的项。 您将通过指定一个和多个列的值来定义集合中的项。 一行中的列将定义一个项。 例如，指定执行进程任务运行的可执行文件以及此任务所用的工作目录的项包含两列，一列列出可执行文件的名称，另一列列出工作目录。 行数决定循环重复的次数。 如果表有 10 行，则循环重复 10 次。  
  
 若要更新执行进程任务的属性，可以使用列索引将变量映射到项列。 枚举器项中定义的第一列的索引值为 0，第二列的索引值为 1，依次类推。 变量值将随着循环的每次重复而更新。 然后，可以通过使用这些变量的属性表达式更新执行进程任务的 `Executable` 和 `WorkingDirectory` 属性。  
  
 **定义 For Each 项集合中的项**  
 为表中的每个列提供值。  
  
> [!NOTE]  
>  在行列中输入值后，新行将自动添加到表中。  
  
> [!NOTE]  
>  如果所提供的值与列数据类型不兼容，则文本以红色显示。  
  
 **列数据类型**  
 列出活动列的数据类型。  
  
 **删除**  
 选择项，再单击 **“删除”** ，即可从列表中删除它。  
  
 **“列”**  
 单击此项可以配置项中的列的数据类型。  
  
 **相关主题：**[“For Each Item 列”对话框 UI 参考](../../2014/integration-services/for-each-item-columns-dialog-box-ui-reference.md)  
  
### <a name="enumerator--foreach-ado-enumerator"></a>Enumerator = Foreach ADO 枚举器  
 您可以使用 Foreach ADO 枚举器枚举变量中存储的 ADO 或 ADO.NET 对象中的行或表。 例如，如果 Foreach 循环包括可将数据集写入变量的脚本任务，则可以使用 Foreach ADO 枚举器枚举数据集中的行。 如果变量包含 ADO.NET 数据集，则可以将枚举器配置为枚举多个表中的行或枚举表。  
  
 **ADO 对象源变量**  
 从列表中选择用户定义的变量，或单击 **“新建变量...”\<**> 创建新变量。  
  
> [!NOTE]  
>  变量必须有 Object 数据类型，否则会发生错误。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
 **第一个表中的行**  
 选择此项将只枚举第一个表中的行。  
  
 **所有表中的行(仅限于 ADO.NET 数据集)**  
 选择此项将枚举所有表中的行。 只有当要枚举的对象是同一 ADO.NET 数据集的所有成员时，此选项才可用。  
  
 **所有表(仅限于 ADO.NET 数据集)**  
 选择此项将只枚举表。  
  
### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>Enumerator = Foreach ADO.NET 架构行集枚举器  
 您可以使用 Foreach ADO.NET 架构行集枚举器枚举指定数据源的架构。 例如，如果 Foreach 循环包括执行 SQL 任务，则可以使用 Foreach ADO.NET 架构行集枚举器枚举架构（例如， **AdventureWorks** 数据库中的列），使用执行 SQL 任务获取架构权限。  
  
 **“连接”**  
 从列表中选择 ADO.NET 连接管理器，或单击 **“新建连接...”\<**> 创建新的 ADO.NET 连接管理器。  
  
> [!IMPORTANT]  
>  ADO.NET 连接管理器必须使用 .NET provider for OLE DB。 如果连接到 SQL Server，则建议使用的访问接口为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **“连接管理器”** 对话框的 **.Net Providers for OleDb** 部分中列出的  Native Client。  
  
 **相关主题：**[ADO 连接管理器](connection-manager/ado-connection-manager.md)、[配置 ADO.NET 连接管理器](configure-ado-net-connection-manager.md)  
  
 **架构**  
 选择要枚举的架构。  
  
 **设置限制**  
 设置要应用于指定架构的限制。  
  
 **相关主题：**[“架构限制”对话框](../../2014/integration-services/schema-restrictions-dialog-box.md)  
  
### <a name="enumerator--foreach-from-variable-enumerator"></a>Enumerator = Foreach 源变量枚举器  
 您可以使用 Foreach 源变量枚举器枚举指定变量中的可枚举对象。 例如，如果 Foreach 循环包括运行查询并在变量中存储结果的执行 SQL 任务，则可以使用 Foreach 源变量枚举器枚举查询结果。  
  
 **变量**  
 从列表中选择变量，或单击“\<新建变量...>”以创建新的变量。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-nodelist-enumerator"></a>Enumerator = Foreach NodeList 枚举器  
 您可以使用 Foreach Nodelist 枚举器枚举一组通过将 XPath 表达式应用到 XML 文件而生成的 XML 节点。 例如，如果 Foreach 循环包括脚本任务，则可以使用 Foreach NodeList 枚举器将满足 XPath 表达式条件的值从 XML 文件传递到脚本任务。  
  
 应用到 XML 文件的 XPath 表达式为外部 XPath 运算，存储于 OuterXPathString 属性中。 如果 XPath 枚举类型设置为`ElementCollection`，Foreach NodeList 枚举器可以将内部 XPath 表达式，存储在 InnerXPathString 属性中的一系列元素中。  
  
 若要了解有关使用 XML 文档和数据的详细信息，请参阅 MSDN Library 中的“[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)”。  
  
 **DocumentSourceType**  
 选择 XML 文档的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 **DocumentSource**  
 如果将 DocumentSourceType 设置为“直接输入”，请提供 XML 代码，或单击省略号按钮 (…) 以通过使用“文档源编辑器”对话框来提供 XML。  
  
 如果将 **DocumentSourceType** 设置为“文件连接”，请选择文件连接管理器，或单击 **“新建连接...”\<**> 创建新的连接管理器。  
  
 **相关主题：**[文件连接管理器](connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将 **DocumentSourceType** 设置为“变量”，请选择现有变量，或单击 **“新建变量...”\<**> 创建新变量。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **EnumerationType**  
 从列表中选择枚举类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Navigator**|使用 XPathNavigator 进行枚举。|  
|**Node**|枚举 XPath 运算返回的节点。|  
|**NodeText**|枚举 XPath 运算返回的文本节点。|  
|`ElementCollection`|枚举 XPath 运算返回的元素节点。|  
  
 **OuterXPathStringSourceType**  
 选择 XPath 字符串的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 `OuterXPathString`  
 如果将 **OuterXPathStringSourceType** 设置为“直接输出”，请提供 XPath 字符串。  
  
 如果将 **OuterXPathStringSourceType** 设置为“文件连接”，请选择文件连接管理器，或单击 **“新建连接...”\<**> 创建新的连接管理器。  
  
 **相关主题：**[文件连接管理器](connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将 **OuterXPathStringSourceType** 设置为“变量”，请选择现有变量，或单击 **“新建变量...”\<**> 创建新变量。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)。  
  
 **InnerElementType**  
 如果**EnumerationType**设置为`ElementCollection`，列表中选择内部元素的类型。  
  
 **InnerXPathStringSourceType**  
 选择内部 XPath 字符串的源类型。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 XML 文档。|  
|**文件连接**|选择包含 XML 文档的文件。|  
|**变量**|将源设置为包含 XML 文档的变量。|  
  
 `InnerXPathString`  
 如果将 **InnerXPathStringSourceType** 设置为“直接输入”，请提供 XPath 字符串。  
  
 如果将 **InnerXPathStringSourceType** 设置为“文件连接”，请选择文件连接管理器，或单击 **“新建连接...”\<**> 创建新的连接管理器。  
  
 **相关主题：**[文件连接管理器](connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果将 **InnerXPathStringSourceType** 设置为“变量”，请选择现有变量，或单击 **“新建变量...”\<**> 创建新变量。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)。  
  
### <a name="enumerator--foreach-smo-enumerator"></a>Enumerator = Foreach SMO 枚举器  
 您可以使用 Foreach SMO 枚举器枚举 SQL Server 管理对象 (SMO) 对象。 例如，如果 Foreach 循环包括执行 SQL 任务，则可以使用 Foreach SMO 枚举器枚举 **AdventureWorks** 数据库中的表并运行计算每个表中行数的查询。  
  
 **“连接”**  
 选择现有 ADO.NET 连接管理器，或单击 **“新建连接...”\<**> 创建新的连接管理器。  
  
 相关的主题：[ADO.NET 连接管理器](connection-manager/ado-net-connection-manager.md)、[配置 ADO.NET 连接管理器](configure-ado-net-connection-manager.md)  
  
 **枚举**  
 指定要枚举的 SMO 对象。  
  
 **“浏览”**  
 选择 SMO 枚举。  
  
 **相关主题：**[“选择 SMO 枚举”对话框](../../2014/integration-services/select-smo-enumeration-dialog-box.md)  
  
### <a name="enumerator--foreach-azure-blob-enumerator"></a>枚举器 = Foreach Azure Blob 枚举器  
 **Azure Blob 枚举器**允许 SSIS 程序包在指定的 blob 位置枚举 blob 文件。 枚举的 blob 文件名可以存储在变量中并用于 Foreach 循环容器内的任务。  
  
 **Azure 存储连接管理器**  
 选择一个现有的 Azure 存储连接管理器或创建一个新的、引用 Azure 存储帐户的连接管理器。  
  
 相关的主题：[Azure 存储连接管理器](connection-manager/azure-storage-connection-manager.md)。  
  
 **Blob 容器名称**  
 指定包含要枚举的 blob 文件的 blob 容器。  
  
 **Blob 目录**  
 指定包含要枚举的 blob 文件的 blob 目录。 Blob 目录是虚拟的层次结构。  
  
 **Blob 名称筛选器**  
 指定用于枚举具有特定名称模式的文件的名称筛选器。 例如 MySheet*.xls\* 将包含如 MySheet001.xls 和 MySheetABC.xlsx 等文件。  
  
 **Blob 时间范围(自/至)筛选器**  
 指定时间范围筛选器。 将枚举在 **TimeRangeFrom** 之后以及在 **TimeRangeTo** 之前修改的文件。  
### <a name="enumerator--foreach-adls-file-enumerator"></a>枚举器 = Foreach ADLS 文件枚举器  
**ADLS 文件枚举器**启用一个 SSIS 包来枚举 adls 具有筛选器的文件。 反斜杠 (`/`)-带前缀的完整路径的枚举的文件可以存储在变量中并用于 Foreach 循环容器内的任务。
  
**AzureDataLakeConnection**  
指定 Azure Data Lake 连接管理器，或创建一个引用 ADLS 帐户的新连接管理器。   
  
**AzureDataLakeDirectory**  
指定要搜索的 ADLS 目录。
  
**FileNamePattern**  
指定文件名筛选器。 将枚举只有其名称与指定的模式匹配的文件。 支持 `*` 和 `?` 通配符。 
  
**SearchRecursively**  
指定是否在指定目录中以递归方式搜索。  
  
## <a name="external-resources"></a>外部资源  
  
-   bidn.com 上的博客文章 [用于各节点列表枚举器的 SSIS](https://go.microsoft.com/fwlink/?LinkId=220671)。  
  
-   博客文章[SSIS 动态设置文件掩码：FileSpec](https://go.microsoft.com/fwlink/?LinkId=238154)，beyondrelational.com 上。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 循环编辑器&#40;常规页&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach 循环编辑器&#40;变量映射页&#41;](../../2014/integration-services/foreach-loop-editor-variable-mappings-page.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [For 循环容器](control-flow/for-loop-container.md)  
  
  
