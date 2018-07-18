---
title: 字词查找转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookuptrans.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b98ce551e69f64a515f58d2b4a0588dabc742ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225827"
---
# <a name="term-lookup-transformation"></a>字词查找转换
  字词查找转换将从转换输入列的文本中提取的字词与引用表中的字词进行匹配， 然后计算出查找表中的字词在输入数据集中出现的次数，并将计数与引用表中的此字词一并写入转换输出的列中。 此转换对于创建基于输入文本并带有词频统计信息的自定义词列表很有用。  
  
 字词查找转换在执行查找之前，先使用与字词提取转换相同的方法从输入列的文本中提取词：  
  
-   将文本分割为句子。  
  
-   将句子分割为词。  
  
-   对词进行规范。  
  
 若要进一步自定义要匹配的字词，可以对字词查找转换进行配置，使其在查找匹配时区分大小写。  
  
## <a name="matches"></a>匹配  
 字词查找使用下列规则执行查找并返回值：  
  
-   如果转换被配置为在查找匹配项时区分大小写，那么它会放弃大小写不相符的匹配项。 例如， *student* 和 *STUDENT* 将视为不同的词。  
  
    > [!NOTE]  
    >  非大写字与位于句首的大写字可为匹配项。 例如，如果 *Student* 是句首词，则 *student* 和 *Student* 之间匹配成功。  
  
-   如果引用表中存在名词或名词短语的复数形式，则查找仅匹配该名词或名词短语的复数形式。 例如， *students* 的所有实例将与 *student*的实例分别计数。  
  
-   如果在引用表中只找到词的单数形式，则该词或短语的单数和复数形式都视为单数形式的匹配项。 例如，如果查找表包含 *student*，而转换找到两个词 *student* 和 *students*，则两个词都将计为查找字词 *student*的匹配项。  
  
-   如果输入列中的文本为还原的名词短语，则规范仅影响名词短语中的最后一个词。 例如， *doctors appointments* 的还原形式为 *doctors appointment*。  
  
 如果查找项包含的字词与引用集中的字词重叠，即一个子字词出现在多个引用记录中，则字词查找转换仅返回一个查找结果。 下面的示例显示查找项包含重叠子字词时的结果。 在本示例中，重叠的子字词为 *Windows*，它出现在两个引用字词中。 但是，转换并不返回两个结果，而仅返回一个引用字词 *Windows*。 第二个引用字词 *Windows 7 Professional*并未返回。  
  
|项|ReplTest1|  
|----------|-----------|  
|输入字词|Windows 7 Professional|  
|引用字词|Windows、Windows 7 Professional|  
|“输出”|Windows|  
  
 字词查找转换可以匹配包含特殊字符的名词和名词短语，而引用表中的数据可能包含这些字符。 特殊字符如下：%、@、&、$、#、\*、:、;、.、“、”、!、?、\<、>、+、=、^、~、|、\\、/、(、)、[、]、{、}、“ 和 ‘。  
  
## <a name="data-types"></a>数据类型  
 字词查找转换只能使用数据类型为 DT_WSTR 或 DT_NTEXT 的列。 如果列包含文本，但不具有这两种数据类型之一，则数据转换可以将数据类型为 DT_WSTR 或 DT_NTEXT 的列添加到数据流，并将列值复制到新列。 然后，数据转换的输出就可以用作字词查找转换的输入。 有关详细信息，请参阅 [Data Conversion Transformation](data-conversion-transformation.md)。  
  
## <a name="configuration-the-term-lookup-transformation"></a>字词查找转换的配置  
 字词查找转换输入列包含 InputColumnType 属性，用于指示该列的用途。 InputColumnType 可能包含以下值：  
  
-   值 0 指示将列仅传递到输出，而不在查找中使用。  
  
-   值 1 指示仅在查找中使用列。  
  
-   值 2 指示将列传递到输出，并在查找中使用列。  
  
 InputColumnType 属性设置为 0 或 2 的转换输出列包含列的 CustomLineageID 属性，该属性包含由上游数据流组件分配给列的沿袭标识符。  
  
 字词查找转换将两列添加到转换输出，默认情况下名为`Term`和`Frequency`。 `Term` 包含查找表中的字词，而 `Frequency` 包含引用表中的字词在输入数据集中出现的次数。 这些列不包含 CustomLineageID 属性。  
  
 查找表必须是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 Access 数据库中的表。 如果将字词提取转换的输出保存到表，则可以使用此表作为引用表，但也可以使用其他表。 必须先将平面文件中、Excel 工作簿或其他源的文本导入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库或 Access 数据库，然后才能使用字词查找转换。  
  
 字词查找转换使用单独的 OLE DB 连接来连接到引用表。 有关详细信息，请参阅 [OLE DB Connection Manager](../../connection-manager/ole-db-connection-manager.md)。  
  
 字词查找转换以完全预缓存模式工作。 运行时，字词查找转换先从引用表中读取字词并将其存储到自己的专用内存，然后再处理转换输入行。  
  
 因为输入列行中的字词可能重复，所以字词查找转换的输出通常具有比转换输入更多的行。  
  
 此转换具有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“字词查找转换编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [字词查找转换编辑器&#40;引用表选项卡&#41;](../../term-lookup-transformation-editor-reference-table-tab.md)  
  
-   [字词查找转换编辑器&#40;字词查找选项卡&#41;](../../term-lookup-transformation-editor-term-lookup-tab.md)  
  
-   [字词查找转换编辑器&#40;高级选项卡&#41;](../../term-lookup-transformation-editor-advanced-tab.md)  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
