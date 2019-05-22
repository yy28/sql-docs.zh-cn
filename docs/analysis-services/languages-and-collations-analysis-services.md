---
title: 语言和排序规则 (Analysis Services) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a66d4665af9980822f5ce4c41ed0b94964fa8c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62634922"
---
# <a name="languages-and-collations-analysis-services"></a>语言和排序规则 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 操作系统提供的语言和排序规则。 **Language** 和 **Collation** 属性首次在安装过程中的实例级别进行设置，但以后可在对象层次结构的不同级别更改。  
  
 在多维模型中 （仅限），可以在数据库或多维数据集上设置这些属性-还可以为多维数据集内的对象创建的翻译上设置它们。 在表格模型中，语言和排序规则均继承于主机操作系统。  
  
 在多维模型中设置 **Language** 和 **Collation** 时，你指定数据模型在处理和查询执行过程中使用的设置，或者你为模型提供多个翻译，以便说外国语的人可用其母语使用此模型。 在对象（数据库、模型或多维数据集）上显式设置 **Language** 和 **Collation** 属性是针对为不同的区域设置配置开发环境和生产服务器的情况，并且你需要确定语言和排序规则与目标环境的语言和排序规则匹配。  
  
##  <a name="bkmk_object"></a> 支持语言和排序规则属性的对象  
 **语言**并**排序规则**属性通常显示在一起的你可以设置**语言**，还可以设置**排序规则**。  
  
 你可在这些对象上设置 **Language** 和 **Collation** ：  
  
-   **实例**。 部署到实例的所有项目将采用实例的语言和排序规则，假设语言和排序规则未定义。 默认情况下，多维模型会让语言和排序规则为空。 部署项目后，生成的数据库和多维数据集获得实例的语言和排序规则。  
  
     最初，语言和排序规则在安装过程中设置，但管理员可在 Management Studio 中对其进行覆盖。 有关详细信息，请参阅 [更改实例上的默认语言或排序规则](#bkmk_defaultLang) 。  
  
-   **数据库**。 要断开继承，你可在项目级别上显式设置数据库中所有多维数据集使用的语言和排序规则。 除非你另外指示，否则数据库中的所有多维数据集将获得你在此级别上指定的语言和排序规则。 如果你定期编写代码并部署到不同区域设置（例如，在中文计算机上开发解决方案，但将其部署到由法国子公司所有的服务器上），在数据库级别设置语言和排序规则是确保解决方案在目标环境中可用的第一步和最重要的一步。 设置这些属性的最佳位置是在项目中（通过项目上的“编辑数据库”  命令）。  
  
-   **数据库维度**。 虽然设计器在数据库维度上显示 **Language** 和 **Collation** 属性，但在此对象上设置属性是没有用的。 数据库维度不用作单独的对象，因此要利用你定义的属性是困难的（虽然不是不可能的）。 在多维数据集中，维度始终从其父多维数据集继承 **Language** 和 **Collation** 。 忽略你可能在单独的数据库维度对象上设置的值。  
  
-   **多维数据集**。 对于主查询结构，你可在多维数据集级别上设置语言和排序规则。 例如，你可能需要在同一个项目中（其中每个多维数据集具有其自己的语言和排序规则）创建多维数据集的多个语言版本，例如英语和中文版本。  
  
     你在此多维数据集上设置的任何语言和排序方式由此多维数据集中包含的所有测量值和维度使用。 更细颗粒度的设置排序规则属性的唯一方法是在维度属性上创建翻译。 否则，假设在属性级别上没有翻译，则每个多维数据集上有一个排序规则。  
  
 此外，你可在 **翻译**对象上让其自行设置 **Language** 。  
  
 当你将翻译添加到多维数据集或维度时，将创建翻译对象。 **Language** 是翻译定义的一部分。 另一方面，**Collation**在多维数据集或更高级别上设置并由所有翻译共享。 这在包含翻译的多维数据集的 XMLA 中很明显，你可从中发现多个语言属性（每个翻译一个属性），但只有一个排序规则。 注意：对维度属性翻译例外，你可覆盖多维数据集排序规则以指定与源列匹配的属性排序规则（数据库引擎支持各列上的排序规则，通常配置各翻译以从不同源列获取成员数据）。 但是，对于所有其他翻译， **Language** 自行使用，无需 **Collation** 推论。 有关详细信息，请参阅 [Analysis Services 中的翻译支持](../analysis-services/translation-support-in-analysis-services.md) 。  
  
##  <a name="bkmk_lang"></a> Analysis Services 中的语言支持  
 **Language** 属性设置在处理过程中使用的对象的区域设置、查询并使用 **Captions** 和 **Translations** 以支持多语情景。 区域设置基于语言标识符（如英语）和区域（如美国或澳大利亚），其进一步优化了数据和时间表示方法。  
  
 在实例级别，该属性在安装过程中设置，并基于 Windows Server 操作系统的语言（37 种语言中的一种，假设安装了语言包）。 你无法更改安装程序中的语言。  
  
 安装后，可使用 Management Studio 或 msmdsrv.ini 配置文件中的服务器属性页覆盖 **Language** 。 你可从更多语言选择，包括 Windows 客户端支持的所有语言。 在服务器实例级别上设置时， **Language** 决定后续部署的所有数据库的区域设置。 例如，如果你将 **Language** 设置为德语，那么部署到实例的所有数据库将具有语言属性 1031，即德语的 LCID。  
  
###  <a name="bkmk_lcid"></a> 语言属性的值是区域设置标识符 (LCID)  
 有效值包括出现在下拉列表中的任何 LCID。 在 Management Studio 和 SQL Server Data Tools 中，LCID 通过等效的字符串表示。 每当显示 **Language** 属性时，出现相同的语言，无论是什么工具。 具有相同的语言列表可确保你可在整个模型中一致地实施和测试翻译。  
  
 虽然 Analysis Services 按名称列出了语言，为属性存储的实际值是 LCID。 当通过编程方式或 msmdsrv.ini 文件设置语言属性时，请使用 [区域设置标识符 (LCID)](http://en.wikipedia.org/wiki/Locale) 作为值。 LCID 是 32 位的值，其包含标识特定语言的语言 ID、排序 ID 和保留位。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用 LCID 指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例和对象的所选语言。  
  
 你可使用十六进制或十进制格式设置 LCID。  “语言”属性的有效值的一些示例包括：  
  
-   0x0409 或 1033 为“英语（美国）”   
  
-   0x0411 或 1041 为“日语”   
  
-   0x0407 或 1031 为“德语（德国）”   
  
-   0x0416 或 1046 为“葡萄牙语（巴西）” 。  
  
 要查看更完整的列表，请参阅 [Microsoft 分配的语言 ID](http://msdn.microsoft.com/goglobal/bb964664.aspx)。 有关详细背景，请参阅 [编码和代码页](/globalization/encoding/encoding-overview)。  
  
> [!NOTE]  
>  **Language** 属性不决定返回系统消息的语言或哪些字符串出现在用户界面中。 错误、警告和消息本地化为 Office 和 Office 365 中支持的所有语言，并当客户端连接指定其中一种支持区域设置时自动使用。  
  
##  <a name="bkmk_collations"></a> Analysis Services 中的排序规则支持  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 仅使用 Windows（版本 _90 和 _100）和二进制排序规则。 它不使用旧的 SQL Server 排序规则。 在整个多维数据集中，使用一个排序规则，属性级别的翻译除外。 有关定义属性翻译的详细信息，请参阅 [Analysis Services 中的翻译支持](../analysis-services/translation-support-in-analysis-services.md)。  
  
 排序规则控制双语言脚本中所有字符串的大小写规则，对象标识符除外。 如果在对象标识符中使用大写和小写字符，请注意对象标识符的大小写区分不是由排序规则决定的，而是由 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]决定。 对于由英语脚本构成的对象标识符，对象标识符始终不区分大小写，无论排序规则是什么。 西里尔字母和其他双语言相反（总是区分大小写）。 有关详细信息，请参阅 [全球化提示和最佳实践 (Analysis Services)](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) 。  
  
 Analysis Services 中的排序规则与 SQL Server 关系数据库引擎的排序规则兼容，假设你以你为每个服务选择的排序选项维护奇偶校验。 例如，如果关系数据库区分重音，你应以相同方式配置多维数据集。 排序规则设置若不同，则会出现问题。 有关示例和解决方法，请参阅 [基于排序规则，Unicode 字符串中的空格有不同处理结果](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)。 有关排序规则和数据库引擎的详细信息，请参阅 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
###  <a name="bkmk_collationtype"></a> 排序规则类型  
 Analysis Services 支持两种排序规则：  
  
-   **Windows 排序规则（版本 _90 和 _100）**  
  
     Windows 排序规则版本是 _90（未标记较早版本）和较新的 _100 版本。 只有 _100 版本在排序规则名称中显示版本号︰  
  
    -   latin1_general  
  
    -   latin1_general_100  
  
     Windows 排序规则基于语言的语言和文化特征对字符排序。 在 Windows 中，由于许多语言共享共同的字母和规则来对字符进行排序和比较，因此排序规则的数量超过用于排序规则的区域设置（或语言）。 例如，33 个 Windows 区域设置（包括所有葡萄牙语和英语 Windows 区域设置）使用 Latin1 代码页 (1252) 并遵循一组公用的字符排序和比较规则。  
  
    > [!NOTE]  
    >  在决定排序规则时，应该与基础数据库所用的排序规则相同。 但是如果可以选择，_100 版本较新并提供了语言上更准确的区域性排序约定。  
  
-   **二级制排列规则（BIN 或 IN2）**  
  
     二进制排序规则按 Unicode 码位排序，不是根据语言值。 例如，当针对 Unicode 数据使用二进制排序规则时，Latin1_General_BIN 和 Japanese_BIN 会生成相同的排序结果。 语言排序可能产生 aAbBcCdD 这样的结果，但二进制排序将是 ABCDabcd，因为所有大写字符的码位都高于小写字符的码位。  
  
###  <a name="bkmk_sortorder"></a> 排序顺序选项  
 排序选项用于优化基于区分大小写、重音、假名和全半角的排序和比较规则。 例如， **的** Collation [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 配置属性的默认值为 Latin1_General_AS_CS，指定使用 Latin1_General 排序规则，并且使用区分重音、区分大小写的排序顺序。  
  
 注意：BIN 和 BIN2 与其他排序选项相斥，如果你要使用 BIN 或 BIN2，应清除排序选项“区分重音”。 类似地，如果选中“BIN2”，则不可使用“区分大小写”、“不区分大小写”、“区分重音”、“不区分重音”、“区分假名”以及“区分全半角”等选项。  
  
 下表说明用于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的 Windows 排序规则排序顺序选项及其关联的后缀。  
  
|排序顺序（后缀）|排序顺序说明|  
|---------------------------|----------------------------|  
|二进制 (_BIN) 或 BIN2 (_BIN2)|SQL Server 中有两种二进制排序规则：旧的 BIN 排序规则和新的 BIN2 排序规则。 在 BIN2 排序规则中，所有字符根据其码位排序。 在 BIN 排序规则中，仅第一个字符按照码位排序，其余字符根据其字节值排序。 （由于 Intel 平台是一个 little endian 体系结构，因此 Unicode 码字符始终以字节对调的形式存储。）<br /><br /> 对于 Unicode 数据类型的二进制排序规则，数据排序将不考虑区域设置。 例如，对 Unicode 数据应用 Latin_1_General_BIN 和 Japanese_BIN，会得到完全相同的排序结果。<br /><br /> 二进制排序顺序既区分大小写，也区分重音。 二进制排序顺序的速度也最快。|  
|区分大小写 (_CS)|区分大写字母和小写字母。 如果选择此项，排序时小写字母将在其对应的大写字母之前。 通过指定 _CI，可以显式设置不区分大小写。 特定于排序规则的大小写设置不适用于对象标识符，例如维度、多维数据集和其他对象的 ID。 有关详细信息，请参阅 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) 。|  
|区分重音 (_AS)|区分重音字符和非重音字符。 例如，“a”和“ấ”视为不同字符。 如果未选择此项，在排序时， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将字母的重音形式和非重音形式视为相同。 通过指定 _AI，可以显式设置不区分重音。|  
|区分假名 (_KS)|区分日语中的两种假名字符类型：平假名和片假名。 如果未选中该选项，则就排序而言， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将平假名字符和片假名字符视为相同。 没有用于不区分假名排序的排序顺序后缀。|  
|区分全半角 (_WS)|区分字符的单字节形式和双字节形式。 如果未选择此项， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将在排序时把同一字符的单字节形式和双字节形式视为相同。 没有用于不区分全半角排序的排序顺序后缀。|  
  
##  <a name="bkmk_defaultLang"></a> 更改实例上的默认语言或排序规则  
 默认语言和排序规则在安装过程中设置，但可在安装后配置过程中进行更改。 更改实例级别的排序规则并不简单，需要满足以下要求：  
  
-   服务重启。  
  
-   更新现有对象的排序规则设置。 创建对象后，排序规则设置继承一次。 对排序规则的后续更改必须手动完成。 有关详细信息，请参阅 [使用 XMLA 更改数据模型中的语言和排序规则](#bkmk_XMLA) 。  
  
-   更新排序规则后，重新处理分隔和维度。  
  
 你可使用 SQL Server Management Studio 或 AMO PowerShell 更改服务器级别的默认语言或排序规则。 或者，可以修改 **\<语言>** 并 **\<CollationName>** 设置在 msmdsrv.ini 文件中，指定语言的 LCID。  
  
1.  在 Management Studio 中，右键单击服务器名 |“属性” | “语言/排序规则”。  
  
2.  选择排序选项。 要选择  “二进制”或 “二进制 2”，首先清除 “区分重音”复选框。  
  
     注意：排序规则和语言是完全独立的设置。 如果你更改其中一个设置，不会筛选另一个的值以显示共同的组合。  
  
3.  更新数据模型以使用新的排序规则（请参见以下部分）。  
  
4.  重新启动服务。  
  
##  <a name="bkmk_cube"></a> 更改多维数据集上的语言或排序规则  
  
1.  在解决方案资源管理器中，在多维数据集设计器中双击多维数据集将其打开。  
  
2.  在“度量值”或“维度”窗格中，选择顶端节点。 每个窗格的顶级对象是多维数据集。  
  
3.  在“属性”中，设置 **Language** 和 **Collation**。 你选择的值将被所有多维数据集对象使用，包括多维数据集维度和度量值，并影响处理和查询操作。  
  
     在多维数据集中的对象上嵌入替代语言和排序规则属性的唯一方法是通过翻译。 有关详细信息，请参阅 [Analysis Services 中的翻译支持](../analysis-services/translation-support-in-analysis-services.md) 。  
  
##  <a name="bkmk_XMLA"></a> 使用 XMLA 更改数据模型中的语言和排序规则  
 创建对象后，继承语言和排序规则设置一次。 对这些属性的后续更改必须手动完成。 快速更改排序规则多个对象的一个方法是在 XMLA 脚本上使用 ALTER 命令。  
  
 默认情况下，排序规则在数据库级别设置一次。 在剩下的对象层次结构中，继承是隐含的。 如果你在多维数据集中的对象上显式设置 **Collation** （这在各维度属性上是允许的），它将出现在 XMLA 定义中。 否则，仅存在顶级排序规则属性。  
  
 在使用 XMLA 修改现有数据库前，请确保你不会引入数据库和用于创建数据库的源文件之间的差异。 例如，你可能需要使用 XMLA 快速更改语言和排序规则进行概念证明测试，但然后跟踪源文件的更改（请参见 [更改多维数据集上的语言或排序规则](#bkmk_cube)），使用现有的操作程序重新部署解决方案。  
  
1.  在 Management Studio 中，右键单击数据库 |**“编写数据库脚本为”** | **“ALTER To”** | “新建查询编辑器窗口”。  
  
2.  用其他值搜索和替换现有语言或排序规则。  
  
3.  按 F5 执行该脚本。  
  
4.  重新处理多维数据集。  
  
##  <a name="bkmk_enablefast1033"></a> 通过 EnableFast1033Locale 加快英语区域设置的性能  
 如果使用英语（美国）语言标识符（0x0409 或 1033）作为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的默认语言，则可以通过设置 **EnableFast1033Locale** 配置属性（一个只能用于该语言标识符的高级配置属性）来获得额外的性能优势。 将该属性的值设置为 **true** 可使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用更快的字符串哈希算法和比较算法。 有关设置配置属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
##  <a name="bkmk_gb18030"></a> Analysis Services 中的 GB18030 支持  
 GB18030 是在中华人民共和国用于对中文字符进行编码的一个单独标准。 在 GB18030 中，字符长度可以是 1 个字节、2 个字节或 4 个字节。 在 Analysis Services 中，处理来自外部源的数据时没有数据转换。 数据仅存储为 Unicode。 在查询时，当查询结果中返回文本数据时，通过 Analysis Services 客户端库（具体指 MSOLAP.dll OLE DB 提供程序）根据客户端 OS 设置执行 GB18030 转换。 数据库引擎还支持 GB18030。 有关详细信息，请参阅 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 的全球化方案](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [全球化提示和最佳实践 (Analysis Services)](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)   
 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
