---
title: 字词提取转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.termextractiontrans.f1
- sql13.dts.designer.termextraction.termextraction.f1
- sql13.dts.designer.termextraction.inclusionexclusion.f1
- sql13.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- word boundaries [Integration Services]
- extracting data [Integration Services]
- sentence boundaries
- word extractions [Integration Services]
- Term Extraction transformation
- tagging words
- normalized data [Integration Services]
- tokenizing text [Integration Services]
- parts of speech [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- stemming words [Integration Services]
ms.assetid: d0821526-1603-4ea6-8322-2d901568fbeb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: acfa92d36166968f4b82b73b5e2d63dcf2dd6370
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725806"
---
# <a name="term-extraction-transformation"></a>字词提取转换

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  字词提取转换从转换输入列的文本中提取字词，然后将这些字词写入转换输出列。 该转换仅处理英文文本，并使用它自身的英语字典和有关英语的语言信息。  
  
 可以用字词提取转换搜索数据集的内容。 例如，包含电子邮件的文本可能会提供关于产品有用的反馈信息，因此，作为分析反馈的一种方法，可以用字词提取转换提取邮件中的讨论主题。  
  
## <a name="extracted-terms-and-data-types"></a>提取的字词和数据类型  
 字词提取转换可以仅提取名词、仅提取名词短语，或者同时提取名词和名词短语。 名词是单个名词；名词短语至少是两个词，其中一个为名词，另一个为名词或形容词。 例如，如果转换使用仅名词选项，则将提取如 *bicycle* 和 *landscape*等字词；如果转换使用名词短语选项，则将提取如 *new blue bicycle*、 *bicycle helmet*和 *boxed bicycles*等字词。  
  
 冠词和代词不提取。 例如，字词提取转换将从文本 *the bicycle* 、 *my bicycle*和 *that bicycle*中提取字词 *bicycle*。  
  
 字词提取转换为所提取的每个字词生成分数。 该分数可以是 TFIDF 值，也可以是原始频率（表示规范的字词在输入中出现的次数）。 不管哪种情况，分数都表示为大于 0 的实数。 例如，TFIDF 分数可能为 0.5 的值，而频率可能为像 1.0 或 2.0 这样的值。  
  
 字词提取转换的输出仅包括两列。 一列包含提取的字词，另一列包含分数。 这两列的默认名称为 **Term** 和 **Score**。 由于输入中的文本列可能包含多个字词，所以字词提取转换输出的行通常比输入的多。  
  
 如果提取字词写入表中，则其他查找转换（如字词查找、模糊查找和查找转换）可以使用它们。  
  
 字词提取转换仅可用于 DT_WSTR 或 DT_NTEXT 数据类型的列中的文本。 如果列包含文本但其数据类型不是这些之一，则可使用数据转换向数据流添加 DT_WSTR 或 DT_NTEXT 数据类型的列并将该列值复制到新列。 然后，数据转换的输出可用作对字词提取转换的输入。 有关详细信息，请参阅 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
## <a name="exclusion-terms"></a>排除字词  
 根据需要，字词提取转换还可以引用包含排除字词（表示转换从数据集中提取字词时应跳过的字词）的表中的列。 当一组字词在特定业务或行业中已标识为不重要（通常是由于该字词出现频率过高，以致其成为干扰词）时，这会很有用。 例如，从包含特定汽车品牌的客户支持信息的数据集中提取字词时，品牌本身由于过于频繁地被提到而变得毫无意义，因此可以排除。 因此，排除列表中的值必须按照正在使用中的数据集进行自定义。  
  
 如果将某一字词添加到排除列表中，则包含该字词的所有字词（不论是单词还是名词短语）也都将被排除。 例如，如果排除列表中包含单个单词 *data*，则包含该单词的所有字词（如 *data*、 *data mining*、 *data integrity*和 *data validation* ）也都将被排除。 如果只希望排除包含单词 *data*的复合词，则必须将这些复合字词显式添加到排除列表中。 例如，如果要提取 *data*，而排除 *data validation*，则需要将 *data validation* 添加到排除列表中，并确保将 *data* 从排除列表中删除。  
  
 引用表必须是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 Access 数据库中的一个表。 字词提取转换使用单独的 OLE DB 连接以便连接到引用表。 有关详细信息，请参阅 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 字词提取转换在完全预缓存模式下工作。 在运行时，字词提取转换从引用表中读取排除字词并将这些字词存储在转换的专用内存中，然后才处理任何转换输入行。  
  
## <a name="extraction-of-terms-from-text"></a>从文本中提取字词  
 若要从文本中提取字词，字词提取转换要执行下列任务。  
  
### <a name="identification-of-words"></a>单词的标识  
 首先，字词提取转换执行下列任务以标识单词：  
  
-   使用英语中的空格、换行符和其他单词终止符将文本分隔为单词。 例如，标点符号（如 *?* 和 *:* 为断字符。  
  
-   保留由连字符或下划线连接的单词。 例如，单词 *copy-protected* 和 *read-only* 保留为一个单词。  
  
-   原封不动地保留包含句点的首字母缩略词。 例如， *A.B.C* Company 将词汇切分为 **ABC** 和 **Company**。  
  
-   拆分带有特殊字符的单词。 例如，单词 *date/time* 提取为 *date* 和 *time*， *(bicycle)* 提取为 *bicycle*，而 C# 则视为 C。特殊字符将被放弃且不能被编入词汇。  
  
-   确认诸如撇号之类的特殊字符何时不应拆分单词。 例如，词 *bicycle's* 不会拆分为两个单词，而是生成一个词 *bicycle* （名词）。  
  
-   拆分时间表达式、货币表达式、电子邮件地址和邮寄地址。 例如，日期 *January 31, 2004* 可分隔为三个标记， *January*、 *31*和 *2004*。  
  
### <a name="tagged-words"></a>带标记的单词  
 第二，字词提取转换将单词标记为下列词类之一：  
  
-   单数形式的名词。 例如， *bicycle* 和 *potato*。  
  
-   复数形式的名词。 例如， *bicycles* 和 *potatoes*。 所有未按异体形式进行归类的复数名词要进行词干提取。  
  
-   单数形式的专有名词。 例如， *April* 和 *Peter*。  
  
-   复数形式的专有名词。 例如， *Aprils* 和 *Peters*。 对于要进行词干提取的专有名词来说，它必须为内部词典（仅限于标准英文单词）的一部分。  
  
-   形容词。 例如， *blue*。  
  
-   对两个事物进行比较的比较级形容词。 例如， *higher* 和 *taller*。  
  
-   标识事物的性质高于或低于至少其他两个事物的形容词最高级。 例如， *highest* 和 *tallest*。  
  
-   数词。 例如， *62* 和 *2004*。  
  
 不属于以上词类的单词将被放弃。 例如，动词和代词将被放弃。  
  
> [!NOTE]  
>  词类是根据统计模型进行标记的，因此标记可能不完全准确。  
  
 如果将字词提取转换配置为仅提取名词，那么将只提取标记为单数或复数形式的名词和专有名词的单词。  
  
 如果将字词提取转换配置为仅提取名词短语，那么标记为名词、专有名词、形容词和数词的单词可以组合成名词短语，但该短语必须包含至少一个标记为单数或复数形式的名词或者专有名词的单词。 例如，名词短语 *highest mountain* 由标记为形容词最高级的单词 (*highest*) 和标记为名词的单词 (*mountain*) 组成。  
  
 如果将字词提取转换配置为可提取名词和名词短语，那么对名词和名词短语的规则都适用。 例如，转换从文本 *many beautiful blue bicycles* 中提取 *bicycle* 和 *beautiful blue bicycle*。  
  
> [!NOTE]  
>  提取的字词仍然受转换所使用的最大字词长度和频率阈值的限制。  
  
### <a name="stemmed-words"></a>词干字词  
 字词提取转换还可以提取名词词干，从而仅提取名词的单数形式。 例如，转换从 *men* 中提取 *man*，从 *mice* 中提取 *mouse*以及从 *bicycles* 中提取 *bicycle*。 转换使用其字典来提取名词词干。 其字典中的动名词将视为名词。  
  
 字词提取转换使用其内部字典，将单词的词干提取为其字典格式，如这些示例中所示。  
  
-   删除名词中的 *s* 。 例如， *bicycles* 变为 *bicycle*。  
  
-   删除名词中的 *es* 。 例如， *stories* 变为 *story*。  
  
-   从字典中检索不规则名词的单数形式。 例如， *geese* 变为 *goose*。  
  
### <a name="normalized-words"></a>规范化的字词  
 对仅因位于句首而大写的字词，字词提取转换一律采用其非首字母大写形式。 例如，在短语 *Dogs chase cats* 和 *Mountain paths are steep*中， *Dogs* 和 *Mountain* 将被规范为 *dog* 和 *mountain*。  
  
 字词提取转换对单词进行规范，从而不将大写和非大写单词视为不同的字词。 例如，在文本 *You see many bicycles in Seattle* 和 *Bicycles are blue*中， *bicycles* 和 *Bicycles* 识别为相同的字词并且转换仅保留 *bicycle*。 内部字典中未列出的专有名词和单词不进行规范。  
  
### <a name="case-sensitive-normalization"></a>区分大小写的规范  
 字词提取转换可以配置为将小写和大写单词视为不同的字词，或者相同字词的不同变体。  
  
-   如果将转换配置为可识别大小写，则 *Method* 和 *method* 这样的字词将被提取为两个不同的字词。 对非句首词的大写单词从不进行规范，并将其标记为专有名词。  
  
-   如果将转换配置为不区分大小写，则如 *Method* 和 *method* 这样的字词将被识别为单个字词的变体。 提取的字词列表可能包括 *Method* 或 *method*，这取决于哪个单词首先出现在输入数据集中。 如果 *Method* 仅因其是句首词而大写，则将以规范形式提取它。  
  
## <a name="sentence-and-word-boundaries"></a>句子和词边界  
 字词提取转换使用下列字符作为句子边界将文本分隔为多个句子：  
  
-   ASCII 换行字符 0x0d（回车符）和 0x0a（换行符）。 若要使用此字符作为句子的边界，则每行中必须有两个或更多的换行字符。  
  
-   连字符 (-)。 若要将此字符用作句子边界，连字符左侧和右侧的字符均不能为字母。  
  
-   下划线 (_)。 若要将此字符用作句子边界，连字符左侧和右侧的字符均不能为字母。  
  
-   小于等于 0x19 或大于等于 0x7b 的所有 Unicode 字符。  
  
-   数字、标点符号和字母字符的组合。 例如， *A23B#99* 返回字词 *A23B*。  
  
-   字符：%、@，&、$、#、\*、;、。、！、？、\<>、+、=、^、~、|、\\/、（、）、[、]、{、}、" 和 '。  
  
    > [!NOTE]  
    >  包括一个或多个句点 (.) 的首字母缩略词不分隔为多个句子。  
  
 然后，字词提取转换使用下列词边界将句子分隔为单词：  
  
-   Space  
  
-   选项卡  
  
-   ASCII 0x0d（回车符）  
  
-   ASCII 0x0a（换行符）  
  
    > [!NOTE]  
    >  如果缩写的单词中包含撇号，如 *we're* 或 *it's*，则在撇号处断词，否则，撇号后的字母将被剪裁掉。 例如， *we're* 拆分为 *we* 和 *'re*，而 *bicycle's* 则剪裁为 *bicycle*。  
  
## <a name="configuration-of-the-term-extraction-transformation"></a>配置字词提取转换  
 文本提取转换使用内部算法和统计模型来生成其结果。 可能需要多次运行字词提取转换并检查结果，以配置转换使其生成用于文本挖掘解决方案的结果类型。  
  
 字词提取转换有一个常规输入、一个输出和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="term-extraction-transformation-editor-term-extraction-tab"></a>字词提取转换编辑器（“字词提取”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“字词提取”** 选项卡，指定包含要提取的文本的文本列。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 通过使用复选框，选择要用于字词提取的单个文本列。  
  
 **术语**  
 为将包含所提取的字词的输出列提供名称。  
  
 **分数**  
 为将包含每个所提取字词的分数的输出列提供名称。  
  
 **配置错误输出**  
 使用[“配置错误输出” ](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式。  
  
## <a name="term-extraction-transformation-editor-exclusion-tab"></a>字词提取转换编辑器（“排除”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“排除”** 选项卡，建立与排除表的连接并指定包含排除字词的列。  
  
### <a name="options"></a>选项  
 **使用排除字词**  
 指示在字词提取过程中是否通过指定包含排除字词的列来排除特定的字词。 如果选择要排除字词，则必须指定以下源属性：  
  
 **“无缓存”**  
 选择现有的 OLE DB 连接管理器，或通过单击“新建”创建新的连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建与数据库的新连接。  
  
 **表或视图**  
 选择包含排除字词的表或视图。  
  
 **列**  
 在表或视图中选择包含排除字词的列。  
  
 **配置错误输出**  
 使用[“配置错误输出” ](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式。  
  
## <a name="term-extraction-transformation-editor-advanced-tab"></a>字词提取转换编辑器（“高级”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“高级”** 选项卡，指定频率、长度等提取属性以及指定是提取字词还是提取短语。  
  
### <a name="options"></a>选项  
 **名词**  
 指定转换仅提取各个名词。  
  
 **名词短语**  
 指定转换仅提取名词短语。  
  
 **名词和名词短语**  
 指定转换既提取名词也提取名词短语。  
  
 **频率**  
 指定分数为字词的频率。  
  
 **TFIDF**  
 指定分数为字词的 TFIDF 值。 TFIDF 分数是字词频率和文档频率倒数的乘积，其定义如下：字词 T 的 TFIDF = (T 的频率) * log( (输入中的行数) / (具有 T 的行数) )  
  
 **频率阈值**  
 指定某个词或短语必须出现多少次以后才对其进行提取。 默认值为 2。  
  
 **字词的最大长度**  
 指定短语的最大长度（字）。 此选项仅影响名词短语。 默认值为 12。  
  
 **使用区分大小写的字词提取**  
 指定是否将提取设置为区分大小写。 默认值为 **False**。  
  
 **配置错误输出**  
 使用[“配置错误输出” ](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [字词查找转换](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  

