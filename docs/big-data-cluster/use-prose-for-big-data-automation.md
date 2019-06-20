---
title: 生成数据整理任务的代码
titleSuffix: Azure Data Studio
description: 本文介绍如何使用 Azure 数据 Studio 中的 PROSE 代码加速器来自动生成的常见数据整理任务代码。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f5406ce0e67322a8f7148fc83b83d0789f27e1ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66770778"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>使用 PROSE 代码 Accelerator 数据 Wrangling

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

PROSE 代码加速器生成你的数据整理任务的可读 Python 代码。 在 Azure Data Studio 中的笔记本中工作时，可以无缝的方式混合与您手动编写的代码生成的代码。 本文概述了如何使用代码加速器。

 > [!NOTE]
 > 程序 Synthesis using Examples 也称为文本信息、 是生成使用 AI 的人工可读代码的 Microsoft 技术。 它会通过分析用户的意向以及数据、 生成多个候选程序，并选择使用排名算法的最佳计划。 若要了解有关 PROSE 技术的详细信息，请访问[PROSE 主页](https://microsoft.github.io/prose/)。

代码加速器可能已使用 Azure Data Studio 预安装。 您可以将其导入笔记本中的任何其他 Python 包等。 按照约定，我们导入为 cx 简称。

```python
import prose.codeaccelerator as cx
```

在当前版本中，代码加速器以智能方式生成 Python 代码的以下任务：

- 读取到 Pandas 数据文件或 Pyspark 数据帧。
- 在数据帧中修复的数据类型。
- 查找正则表达式表示的字符串列表中的模式。

若要获取代码 Accelerator 方法的常规概述，请参阅[文档](https://aka.ms/prose-codeaccelerator-overview)。

## <a name="reading-data-from-a-file-to-a-dataframe"></a>将数据从文件读取到数据帧

通常情况下，读取文件复制到数据帧涉及查看文件的内容并确定要传递到数据加载库的正确参数。 根据文件的复杂性，确定正确的参数可能需要几次迭代。

PROSE 代码 Accelerator 解决此问题： 分析数据文件的结构，并自动生成代码以加载该文件。 在大多数情况下，生成的代码将正确分析数据。 在少数情况下，可能需要调整代码来满足你的需求。

请看下面的示例：

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

上一个代码块将打印以下的 python 代码，以读取带分隔符的文件。 请注意如何 PROSE 自动找出要跳过，标头、 quotechars、 分隔符等的行数。

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

代码加速器可以生成到分隔的负载、 JSON 和固定宽度文件复制到数据帧的代码。 用于读取固定宽度文件`ReadFwfBuilder`选择性地采用它可以解析，以获取的列位置的用户可读的架构文件。 若要了解详细信息，请参阅[文档](https://aka.ms/prose-codeaccelerator-docs)。

## <a name="fixing-data-types-in-a-dataframe"></a>在数据帧中修复的数据类型

它是很常见的 pandas 或 pyspark 使用错误的数据类型的数据帧。 通常情况下，这是由于几个不符合要求列中的值。 因此，整数被读取为浮点型或字符串，并读取以字符串形式的日期。 若要手动修复的数据类型所需的工作量成正比的列数。

可以使用`DetectTypesBuilder`在这些情况下。 它分析的数据，并与其黑色框的方式修复的数据类型，它将生成代码以修复的数据类型。 该代码可作为起始点。 您可以查看、 使用，或根据需要对其进行修改。

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

若要了解详细信息，请参阅[文档](https://aka.ms/prose-codeaccelerator-fixtypes)。

## <a name="identifying-patterns-in-strings"></a>标识字符串中的模式

另一个常见情况是检测来清理或分组的字符串列中的模式。 例如，你可能具有日期的日期列中多个不同的格式。 为了标准化值，你可能想要编写使用正则表达式的条件语句。


|   |“属性”                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-Apr-67      |
| 4 |Maya de Villiers          |19-Mar-60      |

根据的数量和多样性数据中的，编写列中的不同模式的正则表达式可以是非常耗时的任务。 `FindPatternsBuilder`是一个功能强大的代码加速工具，通过生成有关列表的字符串的正则表达式来解决上述问题。

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

以下是由生成的正则表达式`FindPatternsBuilder`的上述数据。

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

除了生成正则表达式，`FindPatternsBuilder`还可以生成聚类分析基于生成正则表达式的值的代码。 它还可以添加一列中的所有值都符合生成正则表达式。 若要了解详细信息，请参阅其他有用的方案，请参阅[文档](https://aka.ms/prose-codeaccelerator-findpatterns)。
