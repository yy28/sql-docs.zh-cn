---
title: 架构.ini 文件（文本文件驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365351724f27205e7d460c757f1268d042cefc76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305508"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 文件（文本文件驱动程序）
使用文本驱动程序时，将使用架构信息文件确定文本文件的格式。 架构信息文件始终名为 Schema.ini，并且始终与文本数据源保存在同一目录中。 架构信息文件向 IISAM 提供有关文件一般格式、列名和数据类型信息以及其他几个数据特征的信息。 访问固定长度数据始终需要架构.ini 文件。 当文本表包含 DateTime、货币或十进制数据时，或者您希望对表中数据的处理进行更多控制的任何时间，应使用 Schema.ini 文件。  
  
> [!NOTE]  
>  文本 ISAM 将从注册表获取初始值，而不是从 Schema.ini 获取初始值。 相同的默认文件格式适用于所有新的文本数据表。 CREATE TABLE 语句创建的所有文件都继承相同的默认格式值，这些值是通过在 **"定义文本格式"** 对话框\<中选择文件格式值（默认>在 **"表"** 列表中选择）来设置的。 如果注册表中的值与 Schema.ini 中的值不同，则注册表中的值将被架构.ini 中的值覆盖。  
  
## <a name="understanding-schemaini-files"></a>了解架构.ini 文件  
 Schema.ini 文件提供有关文本文件中记录的架构信息。 每个架构.ini 条目指定表的五个特征之一：  
  
-   文本文件名  
  
-   文件格式  
  
-   字段名称、宽度和类型  
  
-   字符集  
  
-   特殊数据类型转换  
  
 以下各节讨论这些特征。  
  
## <a name="specifying-the-file-name"></a>指定文件名  
 Schema.ini 中的第一个条目始终是包含在方括号中的文本源文件的名称。 下面的示例说明了文件 Sample.txt 的条目：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定文件格式  
 Schema.ini 中的 **"格式"** 选项指定文本文件的格式。 文本 IISAM 可以从大多数字符分隔文件中自动读取格式。 除了双引号 （） 之外，可以使用任何单个字符作为文件中的分隔符。 架构中的 **"格式"** 设置将覆盖 Windows 注册表中的设置，按文件进行。 下表列出了 **"格式"** 选项的有效值。  
  
|格式说明符|表格式|架构.ini 格式语句|  
|----------------------|------------------|---------------------------------|  
|**选项卡分隔**|文件中的字段由选项卡分隔。|格式=标签限制|  
|**CSV 限制**|文件中的字段按逗号（逗号分隔值）分隔。|格式_CSVDe有限|  
|**自定义分隔**|文件中的字段由您选择输入到对话框中的任何字符分隔。 除双引号 （"） 外，所有内容均允许，包括空白。|格式=分隔（*自定义字符*）<br /><br /> -或-<br /><br /> 未指定分隔符：<br /><br /> 格式=限制）|  
|**固定长度**|文件中的字段长度固定。|格式 =固定长度|  
  
## <a name="specifying-the-fields"></a>指定字段  
 您可以通过两种方式在字符分隔文本文件中指定字段名称：  
  
-   在表的第一行中包括字段名称，并将**ColNameHeader**设置为**True。**  
  
-   按数字指定每列并指定列名称和数据类型。  
  
 您必须按数字指定每列，并为固定长度的文件指定列名称、数据类型和宽度。  
  
> [!NOTE]  
>  架构中的**ColNameHeader**设置将覆盖 Windows 注册表中**的第一个 RowHasNames**设置，逐个文件。  
  
 还可以确定字段的数据类型。 使用**MaxScanRows**选项指示在确定列类型时应扫描多少行。 如果将**MaxScanRows**设置为 0，则扫描整个文件。 架构中的**MaxScanRows**设置将覆盖 Windows 注册表中的设置，按文件进行。  
  
 以下条目指示 Microsoft Jet 应使用表第一行中的数据来确定字段名称，并应检查整个文件以确定使用的数据类型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一个条目使用列号 **（Col**_n_） 选项指定表中的字段，该选项对于字符分隔文件是可选的，并且固定长度文件是必需的。 该示例显示了两个字段的 Schema.ini 条目，一个 10 个字符的客户编号文本字段和一个 30 个字符的客户名称文本字段：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **Col**_n_的语法是：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>备注  
 下表描述了**Col**_n_条目的每个部分。  
  
|参数|说明|  
|---------------|-----------------|  
|*ColumnName*|列的文本名称。 如果列名称包含嵌入空格，则必须将其以双引号括在一起。|  
|*type*|数据类型如下：<br /><br /> **微软 Jet 数据类型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> 货币<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Text<br /><br /> 备忘录<br /><br /> **ODBC 数据类型**字符（与文本相同）<br /><br /> 浮动（与双花相同）<br /><br /> 整数（与短数相同）<br /><br /> 长字符（与备忘录相同）<br /><br /> *日期格式*|  
|**宽度**|文本字符串值`Width`。 指示以下数字指定列的宽度（对于字符分隔文件可选;固定长度文件需要）。|  
|*#*|指定列宽度的整数值（如果指定**了"宽度**"，则需要）。|  
  
## <a name="selecting-a-character-set"></a>选择字符集  
 您可以从两个字符集中选择：ANSI 和 OEM。 架构中的**字符集**设置将覆盖 Windows 注册表中的设置，逐个文件。 下面的示例显示了将字符设置为 ANSI 的架构.ini 条目：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定数据类型格式和转换  
 Schema.ini 文件包含多个选项，可用于指定数据的转换或显示方式。 下表列出了每个选项。  
  
|选项|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以设置为指示日期和时间的格式字符串。 如果导入/导出中的所有日期/时间字段都使用相同的格式处理，则应指定此条目。 除 A.M. 外，所有 Microsoft Jet 格式 和 P.M. 。 如果没有格式字符串，则使用 Windows 控制面板短日期图片和时间选项。|  
|**十进制符号**|可以设置为用于将整数与数字的小数部分分隔的任何单个字符。|  
|**数字位数**|指示数字小数部分中的小数位数。|  
|**数字领先零**|指定小于 1 和小于 -1 的小数值是否应包含前导零;如果十进制值小于 1，小于 -1 值是否应包含前导零。此值可以是 False（无前导零）或 True。|  
|**CurrencySymbol**|指示可用于文本文件中货币值的货币符号。 示例包括美元符号 （$） 和 Dm。|  
|**货币货币格式**|可以设置为以下任意值：<br /><br /> - 无分隔的货币符号前缀 （$1）<br />- 货币符号后缀，无分离 （1$）<br />- 带有一个字符分隔的货币符号前缀 （$ 1）<br />- 带有一个字符分隔（1 美元）的货币符号后缀|  
|**货币数字**|指定用于货币金额小数部分的数字数。|  
|**货币内格罗格式**|可以是以下值之一：<br /><br /> - （1美元）<br />- -$1<br />- $-1<br />- $1-<br />- （1美元）<br />- -1$<br />- 1-$<br />- 1美元-<br />- -1 $<br />- -$ 1<br />- 1 $-<br />- $ 1-<br />- $ -1<br />- 1- $<br />- （1美元）<br />- （1 $）<br /><br /> 此示例显示美元符号，但应在实际程序中将其替换为相应的**货币符号**值。|  
|**货币千符号**|指示可用于将文本文件中的货币值分隔成千计的单字符符号。|  
|**货币十进制符号**|可以设置为任何单个字符，用于将整体与货币金额的小数部分分开。|  
  
> [!NOTE]  
>  如果省略了项，则使用 Windows 控制面板中的默认值。
