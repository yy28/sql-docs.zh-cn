---
title: Schema.ini 文件（文本文件驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305508"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 文件（文本文件驱动程序）
使用文本驱动程序时，文本文件的格式是使用架构信息文件确定的。 架构信息文件始终命名为 schema.ini，并始终保存在与文本数据源相同的目录中。 架构信息文件为 IISAM 提供了有关文件的常规格式、列名称和数据类型信息以及其他一些数据特征的信息。 访问固定长度的数据始终需要一个架构 .ini 文件。 当您的文本表包含日期时间、货币或小数数据时，或者您希望更好地控制表中数据的处理时，应使用 schema.ini 文件。  
  
> [!NOTE]  
>  文本 ISAM 将从注册表而不是从 schema.ini 获取初始值。 同一默认文件格式适用于所有新的文本数据表。 通过在 "**定义文本格式**" 对话框中选择 "文件格式" 值，并\<在 "**表**" 列表中选择了默认的>，CREATE TABLE 语句创建的所有文件都将继承这些默认格式值。 如果注册表中的值与 schema.ini 中的值不同，则注册表中的值将被 schema.ini 中的值覆盖。  
  
## <a name="understanding-schemaini-files"></a>了解 schema.ini 文件  
 架构 .ini 文件提供有关文本文件中的记录的架构信息。 每个 schema.ini 条目指定了表中的五个特征之一：  
  
-   文本文件名称  
  
-   文件格式  
  
-   字段名称、宽度和类型  
  
-   字符集  
  
-   特殊数据类型转换  
  
 以下各节将讨论这些特性。  
  
## <a name="specifying-the-file-name"></a>指定文件名  
 Schema.ini 中的第一个条目始终是括在方括号内的文本源文件的名称。 下面的示例说明了文件示例的条目：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定文件格式  
 Schema.ini 中的**format**选项指定了文本文件的格式。 文本 IISAM 可以从大多数字符分隔文件自动读取格式。 您可以使用任何单个字符作为文件中的分隔符（双引号（"）除外）。 Schema.ini 中的**格式**设置将覆盖 Windows 注册表中按文件的设置。 下表列出了**Format**选项的有效值。  
  
|格式说明符|表格式|Schema.ini 格式语句|  
|----------------------|------------------|---------------------------------|  
|**制表符分隔**|文件中的字段由选项卡分隔。|Format = TabDelimited|  
|**CSV 分隔**|文件中的字段以逗号分隔（逗号分隔）。|Format = CSVDelimited|  
|**自定义分隔**|文件中的字段由您选择输入到对话框中的任何字符分隔。 除双引号（"）之外的所有都允许使用，其中包括空白。|格式 = 分隔符（*自定义字符*）<br /><br /> \- 或 -<br /><br /> 未指定分隔符：<br /><br /> 格式 = 分隔（）|  
|**固定长度**|文件中的字段的长度是固定的。|Format = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定字段  
 可以通过两种方式在字符分隔的文本文件中指定字段名称：  
  
-   在表的第一行中包括字段名称，并将**ColNameHeader**设置为**True。**  
  
-   按编号指定每列，并指定列名称和数据类型。  
  
 必须按编号指定每列，并指定列名称、数据类型和固定长度文件的宽度。  
  
> [!NOTE]  
>  Schema.ini 中的**ColNameHeader**设置将覆盖 Windows 注册表中按文件的**FirstRowHasNames**设置。  
  
 还可以确定这些字段的数据类型。 使用**MaxScanRows**选项可指示在确定列类型时应扫描的行数。 如果将**MaxScanRows**设置为0，则将扫描整个文件。 Schema.ini 中的**MaxScanRows**设置将覆盖 Windows 注册表中按文件的设置。  
  
 下面的条目指出，Microsoft Jet 应使用表的第一行中的数据来确定字段名称，应检查整个文件以确定所使用的数据类型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一项通过使用列号（**列**_n_）选项指定表中的字段，该选项对于字符分隔文件是可选的，而对于固定长度文件则是必需的。 该示例显示了两个字段的 schema.ini 条目：一个10个字符的 CustomerNumber 文本字段和一个30个字符的 CustomerName 文本字段：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **列**_n_的语法为：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>备注  
 下表描述了**Col**_n_条目的每个部分。  
  
|参数|说明|  
|---------------|-----------------|  
|*ColumnName*|列的文本名称。 如果列名中包含嵌入的空格，则必须用双引号将其引起来。|  
|*type*|数据类型如下所示：<br /><br /> **Microsoft Jet 数据类型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> 货币<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Text<br /><br /> 备忘录<br /><br /> **ODBC 数据类型**Char （与文本相同）<br /><br /> Float （与 Double 相同）<br /><br /> 整数（与 Short 相同）<br /><br /> LongChar （与备注相同）<br /><br /> 日期*日期格式*|  
|**宽度**|文本字符串值`Width`。 指示以下数字指定列的宽度（对于字符分隔文件是可选的; 对于固定长度的文件，则为可选）。|  
|*#*|指定列的宽度的整数值（如果指定了**width** ，则为必需的）。|  
  
## <a name="selecting-a-character-set"></a>选择字符集  
 可以从两个字符集中进行选择： ANSI 和 OEM。 Schema.ini 中的**CharacterSet**设置将覆盖 Windows 注册表中按文件的设置。 以下示例显示了将字符集设置为 ANSI 的 schema.ini 条目：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定数据类型格式和转换  
 Schema.ini 文件包含多个选项，您可以使用这些选项指定数据的转换或显示方式。 下表列出了其中的每个选项。  
  
|选项|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以设置为表示日期和时间的格式字符串。 如果导入/导出中的所有日期/时间字段都用相同的格式处理，则应指定此项。 除 A.M 以外的所有 Microsoft Jet 格式 和 P.M. 。 如果没有格式字符串，则使用 Windows 控制面板的短日期图片和时间选项。|  
|**DecimalSymbol**|可以设置为任何单个字符，用于分隔数字的小数部分中的整数。|  
|**NumberDigits**|指示数字小数部分的小数位数。|  
|**NumberLeadingZeros**|指定小于1且大于-1 的小数值是否应包含前导零。此值可以是 False （无前导零）或 True。|  
|**CurrencySymbol**|指示可用于文本文件中货币值的货币符号。 示例包括美元符号（$）和 Dm。|  
|**CurrencyPosFormat**|可以设置为以下任一值：<br /><br /> -不带分隔的货币符号前缀（$1）<br />-不带分隔的货币符号后缀（$1）<br />-包含一个字符分隔的货币符号前缀（$1）<br />-包含一个字符分隔的货币符号后缀（$1）|  
|**CurrencyDigits**|指定用于货币金额的小数部分的位数。|  
|**CurrencyNegFormat**|可以是以下其中一个值：<br /><br /> -（$1）<br />--$1<br />--1<br />-$1-<br />-（$1）<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />--1<br />-1-$<br />-（$1）<br />-（$1）<br /><br /> 此示例显示美元符号，但应将其替换为实际程序中的相应**CurrencySymbol**值。|  
|**CurrencyThousandSymbol**|指示可用于分隔文本文件中的货币值的单字符符号。|  
|**CurrencyDecimalSymbol**|可以设置为一个字符，该字符用于将整个与货币金额的小数部分分隔开。|  
  
> [!NOTE]  
>  如果省略某个条目，则使用 Windows 控制面板中的默认值。
