---
title: Schema.ini 文件 （文本文件驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd95329c91c69af38b1ffc7951191498fcc40479
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987945"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 文件（文本文件驱动程序）
使用文本驱动程序时，使用架构信息文件来确定文本文件的格式。 架构信息文件是始终命名为 Schema.ini，始终放置在文本数据源所在的同一目录中。 架构信息文件提供了有关的信息的一般格式的文件、 列名称和数据类型信息和几个其他数据特征 IISAM。 Schema.ini 文件始终都需要访问固定长度的数据。 当文本表包含日期时间、 货币或小数数据或只要您希望更好地控制的表中的数据处理时，应使用 Schema.ini 文件。  
  
> [!NOTE]  
>  从注册表中，不能从 Schema.ini 文本 ISAM 将获取初始值。 相同的默认文件格式适用于所有新的文本数据表格。 由 CREATE TABLE 语句创建的所有文件都会都继承这些相同的默认格式值，该值通过选择文件格式中的值来设置**定义文本格式**带有对话框\<默认 >中选择**表**列表。 如果在注册表中的值不同于 Schema.ini 中的值，从 Schema.ini 的值将覆盖注册表中的值。  
  
## <a name="understanding-schemaini-files"></a>了解 Schema.ini 文件  
 Schema.ini 文件提供有关在文本文件中的记录的架构信息。 每个 Schema.ini 条目指定的表的五个特征之一：  
  
-   文本文件名称  
  
-   文件格式  
  
-   字段名称、 宽度和类型  
  
-   字符集  
  
-   特殊数据类型转换  
  
 以下各节讨论这些特征。  
  
## <a name="specifying-the-file-name"></a>指定的文件的名称  
 Schema.ini 的第一个项始终是用方括号括起来的文本源文件的名称。 下面的示例演示了文件 Sample.txt 的条目：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定的文件格式  
 **格式**中 Schema.ini 选项指定的文本文件格式。 文本 IISAM 可以从最字符分隔的文件自动读取格式。 除双引号 （"） 文件中的分隔符，可以使用任何单个字符。 **格式**Schema.ini 中的设置将替代在 Windows 注册表中，文件的文件的设置。 下表列出了有效值**格式**选项。  
  
|格式说明符|表格式|Schema.ini 格式语句|  
|----------------------|------------------|---------------------------------|  
|**制表符分隔**|由制表符分隔文件中的字段。|格式 = TabDelimited|  
|**CSV 分隔**|文件中的字段由逗号 （以逗号分隔值） 分隔。|格式 = CSVDelimited|  
|**自定义分隔符**|选择输入到对话框中的任何字符分隔文件中的字段。 除双引号 （"） 外所有允许，包括保留为空。|格式 = 带分隔符 (*自定义字符*)<br /><br /> -或-<br /><br /> 与任何指定的分隔符：<br /><br /> 格式 = 带分隔符 （）|  
|**固定的长度**|在文件中的字段是固定长度。|格式 = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定的字段  
 可以在两种方法中的字符分隔文本文件中指定字段名称：  
  
-   表的第一行中包括的字段名称并将设置**ColNameHeader**到 **，则返回 True。**  
  
-   指定数量的每个列，然后将指定的列名称和数据类型。  
  
 您必须指定数量的每个列，并指定列名称、 数据类型和固定长度的文件的宽度。  
  
> [!NOTE]  
>  **ColNameHeader** Schema.ini 重写中设置**FirstRowHasNames**设置在 Windows 注册表中，文件的文件。  
  
 此外可确定字段的数据类型。 使用**MaxScanRows**选项以指示确定的列类型时，应扫描行数。 如果您设置**MaxScanRows**为 0，扫描整个文件。 **MaxScanRows** Schema.ini 中的设置将替代在 Windows 注册表中，文件的文件的设置。  
  
 以下项均表示 Microsoft Jet 应使用的表的第一行中的数据来确定字段名称，并应检查以确定的数据的整个文件使用的类型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一个条目将在表中的字段指定使用的列号 (**Col**_n_) 选项，这是可选的分隔字符的文件和所需的固定长度的文件。 该示例显示了两个字段，10 个字符列可以是 CustomerNumber 文本字段和 30 个字符 CustomerName 文本字段的 Schema.ini 项：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 语法**Col**_n_是：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>备注  
 下表描述的每个部分**Col**_n_条目。  
  
|参数|描述|  
|---------------|-----------------|  
|*ColumnName*|文本列的名称。 如果列名称包含嵌入的空格，则必须将其括在双引号。|  
|*type*|数据类型是按如下所示：<br /><br /> **Microsoft Jet 的数据类型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> Currency<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Text<br /><br /> 备忘录<br /><br /> **ODBC 数据类型**Char （与文本相同）<br /><br /> Float （与 Double 相同）<br /><br /> 整数 （相同短格式）<br /><br /> LongChar （等同于备注）<br /><br /> 日期*日期格式*|  
|宽度 |文本字符串值`Width`。 指示下面的编号，将指定的列的宽度 （对于字符分隔的文件是可选的; 对于固定长度的文件所需）。|  
|*#*|指定列的宽度的整数值 (需要**宽度**指定)。|  
  
## <a name="selecting-a-character-set"></a>选择的字符集  
 您可以选择从两个字符集：ANSI 和 OEM。 **CharacterSet** Schema.ini 中的设置将替代在 Windows 注册表中，文件的文件的设置。 下面的示例显示了设置设置为 ANSI 字符的 Schema.ini 条目：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定数据类型格式和转换  
 Schema.ini 文件包含几个选项，可用于指定数据转换或显示方式。 下表列出了每个选项。  
  
|Option|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以设置为一个格式字符串，表示日期和时间。 如果使用相同的格式处理中导入/导出的所有日期/时间字段，则应指定此项。 所有 Microsoft Jet 格式，除了上午 和下午 支持。 如果没有任何格式字符串，使用 Windows 控制面板短日期图片和时间选项。|  
|**DecimalSymbol**|可以设置为任何单个字符，用于分隔和数字的小数部分的整数。|  
|**NumberDigits**|指示一个数字的小数部分的十进制数字的数字。|  
|**NumberLeadingZeros**|指定十进制值小于 1 和多个为-1 是否应包含前导零。此值可以是任一 False （无前导零） 或 True。|  
|**CurrencySymbol**|指示可以用于在文本文件中的货币值的货币符号。 示例包括美元符号 （$） 和数据挖掘。|  
|**CurrencyPosFormat**|可以设置为以下值之一：<br /><br /> 货币符号前缀，并且没有分隔 ($1)<br />具有任何单独的货币符号后缀 (1$)<br />用一个字符分隔 ($ 1) 的货币符号前缀<br />用一个字符分隔的货币符号后缀 (1 $)|  
|**CurrencyDigits**|指定用于货币金额的小数部分的位数。|  
|**CurrencyNegFormat**|可以是以下值之一：<br /><br /> -   ($1)<br />-   -$1<br />-   $-1<br />-   $1-<br />-   (1$)<br />-   -1$<br />-$ 1<br />-   1$-<br />--1 $<br />-   -$ 1<br />-1-<br />-   $ 1-<br />-   $ -1<br />-$ 1<br />-   ($ 1)<br />-   (1 $)<br /><br /> 此示例演示美元符号，但应将其替换适当**CurrencySymbol**实际程序中的值。|  
|**CurrencyThousandSymbol**|指示可以由数以千计的分隔文本文件中的货币值的单字符符号。|  
|**CurrencyDecimalSymbol**|可以设置为任何单个字符，用于整个分开货币金额的小数部分。|  
  
> [!NOTE]  
>  如果省略一个条目，使用 Windows 控制面板中的默认值。
