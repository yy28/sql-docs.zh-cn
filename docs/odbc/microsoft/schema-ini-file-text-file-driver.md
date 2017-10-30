---
title: "Schema.ini 文件 （文本文件驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 709df0de2e0191c0f03026afdad7b8e9b8480cae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 文件 （文本文件驱动程序）
当使用文本驱动程序时，使用的架构信息文件来确定文本文件的格式。 架构信息文件始终名为 Schema.ini，会始终保留在文本数据源所在的目录。 架构信息文件提供了有关的一般格式的文件、 列名称和数据类型信息和若干其他数据特性的信息 IISAM。 Schema.ini 文件始终是必需的访问固定长度的数据。 当文本表包含日期时间、 货币或小数数据或随时根据需要更好地控制的表中的数据的处理时，应使用 Schema.ini 文件。  
  
> [!NOTE]  
>  从注册表中，不是从 Schema.ini 文本 ISAM 将获取初始值。 相同的默认文件格式适用于所有新的文本数据表格。 CREATE TABLE 语句创建的所有文件都会都继承这些相同的默认格式值，通过选择文件中的值设置格式设置**定义文本格式** 癸杠\<默认 > 选择**表**列表。 如果注册表中的值不同于 Schema.ini 中的值，则将从 Schema.ini 的值覆盖注册表中的值。  
  
## <a name="understanding-schemaini-files"></a>了解 Schema.ini 文件  
 Schema.ini 文件提供有关在文本文件中的记录的架构信息。 每个 Schema.ini 条目指定的表的五个特征之一：  
  
-   文本文件名称  
  
-   文件格式  
  
-   字段名称、 宽度和类型  
  
-   字符集  
  
-   特殊的数据类型转换  
  
 以下各节讨论这些特征。  
  
## <a name="specifying-the-file-name"></a>指定的文件名称  
 Schema.ini 中的第一个条目始终是用方括号括起来的文本源文件的名称。 下面的示例阐释了 Sample.txt 的文件的条目：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定的文件格式  
 **格式**中 Schema.ini 选项指定的文本文件的格式。 文本 IISAM 可以格式自动从文件中读取最字符分隔。 任何单个字符可用作除双引号 （"） 文件中的分隔符。 **格式**Schema.ini 中的设置将替代 Windows 注册表中，按文件中的设置。 下表列出的有效值**格式**选项。  
  
|格式说明符|表格式|Schema.ini Format 语句|  
|----------------------|------------------|---------------------------------|  
|**制表符分隔**|由制表符分隔文件中的字段。|格式 = TabDelimited|  
|**CSV 分隔**|文件中的字段由逗号 （以逗号分隔值） 分隔。|格式 = CSVDelimited|  
|**自定义分隔符**|由你选择输入到对话框中的任何字符分隔文件中的字段。 除双引号 （"） 允许所有，包括空白。|格式 = 带分隔符 (*自定义字符集*)<br /><br /> - 或 -<br /><br /> 无分隔符替换为指定：<br /><br /> 格式 = 分隔 （）|  
|**固定的长度**|文件中的字段均为固定长度。|格式 = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定的字段  
 在字符分隔的文本文件，两种方式中，你可以指定字段名称：  
  
-   表的第一行中包括的字段名称并将设置**ColNameHeader**到**True。**  
  
-   指定每个列数和指定的列名称和数据类型。  
  
 必须指定每个列数和指定的列名称、 数据类型和长度固定文件的宽度。  
  
> [!NOTE]  
>  **ColNameHeader** Schema.ini 重写中设置**FirstRowHasNames**设置在 Windows 注册表中，文件的文件。  
  
 此外可确定字段的数据类型。 使用**MaxScanRows**选项以指示确定的列类型时，应进行扫描行数。 如果你设置**MaxScanRows**为 0，扫描整个文件。 **MaxScanRows** Schema.ini 中的设置将替代 Windows 注册表中，按文件中的设置。  
  
 以下条目表示 Microsoft Jet 是应该使用表的第一行中的数据来确定字段名称，应检查以确定数据的整个文件使用类型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一个条目使用的列号指定表中的字段 (**Col***n*) 选项，这是可选的字符分隔的文件和固定长度的文件需要。 该示例演示两个字段、 10 个字符 CustomerNumber 文本字段和 30 个字符 CustomerName 文本字段的 Schema.ini 项：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 语法**Col** * n *是：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>注释  
 下表介绍每个部分的**Col** * n *条目。  
  
|参数|Description|  
|---------------|-----------------|  
|*列名称*|列的文本名称。 如果列名称包含嵌入的空格，必须将它括在双引号中。|  
|*type*|数据类型如下所示：<br /><br /> **Microsoft Jet 数据类型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> 货币<br /><br /> Single<br /><br /> 双精度<br /><br /> DateTime<br /><br /> Text<br /><br /> 备忘录<br /><br /> **ODBC 数据类型**Char （与文本相同）<br /><br /> Float （与 Double 相同）<br /><br /> 整数 （短格式相同）<br /><br /> LongChar （等同于备注）<br /><br /> 日期*日期格式*|  
|**宽度**|文本字符串值`Width`。 指示下面的编号，指定列的宽度 （对于字符分隔的文件是可选的; 固定长度的文件需要）。|  
|*#*|指定列的宽度的整数值 (如果存在**宽度**指定)。|  
  
## <a name="selecting-a-character-set"></a>选择一种字符集  
 你可以选择从两个字符集： ANSI 和 OEM。 **CharacterSet** Schema.ini 中的设置将替代 Windows 注册表中，按文件中的设置。 下面的示例演示设置设置为 ANSI 字符的 Schema.ini 条目：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定数据类型格式和转换  
 Schema.ini 文件包含可用于指定如何转换或显示数据的几个选项。 下表列出了其中每个选项。  
  
|选项|Description|  
|------------|-----------------|  
|**DateTimeFormat**|可以将设置为指示日期和时间格式字符串。 如果在导入/导出的所有日期/时间字段的都处理相同的格式，则应该指定此项。 所有 Microsoft Jet 格式，除了上午 和下午 支持。 如果没有任何格式字符串，将使用 Windows 控制面板短日期图片和时间选项。|  
|**DecimalSymbol**|可以设置为任何单个字符，用于分隔从一个数字的小数部分的整数。|  
|**NumberDigits**|指示一个数字的小数部分的十进制数字的数字。|  
|**NumberLeadingZeros**|指定了小于 1 和多个为-1 的一个十进制值是否应包含前导零。此值可以为 False （无前导零） 或 True。|  
|**CurrencySymbol**|指示可以用于货币值的文本文件中的货币符号。 示例包括美元符号 （$） 和数据挖掘。|  
|**CurrencyPosFormat**|可以设置为任何以下值：<br /><br /> 没有分隔 ($1) 的货币符号前缀<br />没有分隔的货币符号后缀 (1$)<br />货币符号前缀，以及一个字符分隔 ($ 1)<br />的用一个字符分隔货币符号后缀 (1 $)|  
|**CurrencyDigits**|指定用于货币金额的小数部分的数字个数。|  
|**CurrencyNegFormat**|可以是以下值之一：<br /><br /> -   ($1)<br />-   –$1<br />-   $–1<br />-   $1–<br />-   (1$)<br />-   –1$<br />-   1–$<br />-   1$–<br />-   –1 $<br />-   –$ 1<br />-   1 $–<br />-   $ 1–<br />-   $ –1<br />-   1– $<br />-   ($ 1)<br />-   (1 $)<br /><br /> 此示例演示美元符号，但应将其替换为相应**CurrencySymbol**实际的程序中的值。|  
|**CurrencyThousandSymbol**|指示可以用于分隔的文本文件中的货币值的千位的单字符符号。|  
|**CurrencyDecimalSymbol**|可以设置为任何单个字符，用于整个分开货币金额的小数部分。|  
  
> [!NOTE]  
>  如果省略一个条目，使用 Windows 控制面板中的默认值。

