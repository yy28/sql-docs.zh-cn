---
title: dwloader 并行数据仓库的命令行加载程序
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: '**dwloader**是一个并行数据仓库 (PDW) 命令行工具，将表行批量加载到现有表。'
ms.date: 11/04/2016
ms.topic: article
ms.assetid: f79b8354-fca5-41f7-81da-031fc2570a7c
caps.latest.revision: 90
ms.openlocfilehash: 83d04928aa0c8f7fe0156f557466edccc36470dd
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="dwloader-command-line-loader"></a>dwloader 命令行加载程序
**dwloader**是一个并行数据仓库 (PDW) 命令行工具，将表行批量加载到现有表。 当加载行时，可以将所有行都添加到表的末尾 (*追加模式*或*fastappend 模式*)、 追加新行和更新现有行 (*upsert 模式*)，或删除所有现有的行之前加载，然后将所有行都插入空表 (*重新加载模式*)。  
  
**用于加载数据的过程**  
  
1.  准备源数据。  
  
    使用你自己 ETL 过程来创建你想要加载的源数据。 源数据必须格式化为与目标表的架构匹配。 将源数据存储到一个或多个文本文件并将文本文件复制到你加载服务器上的相同目录。 有关加载服务器的信息，请参阅[获取和配置加载的服务器](acquire-and-configure-loading-server.md)  
  
2.  准备加载选项。  
  
    确定你将使用哪些加载选项。 在配置文件中存储的加载选项。 将配置文件复制到你加载服务器上的本地位置。 **Dwloader**本主题中描述了配置选项。  
  
3.  准备负载故障选项。  
  
    决定要如何**dwloader**以处理加载失败的行。 若要执行负载， **dwloader**首先将数据加载到临时表，然后将数据传输到目标表。 加载程序将数据加载到临时表，因为它跟踪加载失败的行的数。 例如，将无法加载的格式不正确的行。 失败的行复制到拒绝文件。 默认情况下，负载中止后首次拒绝除非你指定不同的拒绝阈值。  
  
4.  安装**dwloader**。  
  
    如果尚未安装，请安装 dwloader 加载服务器上。 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  运行**dwloader**。  
  
    登录到加载服务器和运行可执行文件**dwloader.exe**和相应的命令行选项。  
  
6.  验证结果。  
  
    你可以检查失败的行 （使用-R 指定） 的文件以查看是否未能加载的任何行。 如果此文件为空，所有行成功都加载。 **dwloader**是事务性的所以如果任何单步执行将失败 （除被拒绝的行），则所有步骤将都回滚到其初始状态。  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>语法  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]   
}  
```  
  
## <a name="arguments"></a>参数  
**-h**  
显示简单的帮助信息使用加载程序。 如果未不指定任何其他命令行参数，仅显示帮助。  
  
**-U** *login_name*  
具有适当的权限以执行加载的有效 SQL Server 身份验证登录名。  
  
**-P** *password*  
SQL Server 身份验证的密码*login_name*。  
  
**-W**  
使用 Windows 身份验证。 (无*login_name*或*密码*需要。) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
使用参数文件， *parameter_file_name*，代替命令行参数。 *parameter_file_name*可以包含除任何命令行参数*user_name*和*密码*。 如果在命令行和参数文件中指定参数，则命令行重写文件的参数。  
  
参数文件包含一个参数，而不**-**前缀，每行。  
  
示例：  
  
`rt=percentage`  
  
`rv=25`  
  
**-S***target_appliance*  
指定 SQL Server PDW 设备将接收加载的数据。  
  
*有关 Infiniband 连接*， *target_appliance*被指定为 < 设备-名称 >-SQLCTL01。 若要配置此命名的连接，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
为以太网连接*target_appliance*是控制节点群集的 IP 地址。  
  
如果省略，dwloader 默认为安装 dwloader 时指定的值。 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.*[*schema*].*table_name*  
目标表由三部分名称。  
  
**-I***source_data_location*  
若要加载的一个或多个源文件的位置。 每个源文件必须为文本文件或使用 gzip 压缩的文本文件。 只有一个源文件可以压缩到每个 gzip 文件。  
  
若要设置格式的源文件：  
  
-   源文件的格式必须根据加载选项。  
  
-   在源文件中的每个行包含一个表行的数据。 源数据必须与目标表的架构匹配。 列顺序和数据类型还必须匹配。 行中的每个字段表示目标表中的列。  
  
-   默认情况下，字段是可变长度和由分隔符分隔。 若要指定的分隔符类型，使用 < variable_length_column_options > 命令行选项。 若要指定固定的长度字段，请使用 < fixed_width_column_options > 命令行选项。  
  
若要指定的源数据位置：  
  
-   源数据位置可以是网络路径或加载服务器上的目录的本地路径。  
  
-   若要指定目录中的所有文件，输入目录路径后, 跟 * 通配符字符。  加载程序不会从任何子目录中的源数据位置加载文件... 加载程序错误时的目录存在于 gzip 文件。  
  
-   若要指定的某些文件的目录中，使用字符的组合和 * 通配符。  
  
若要使用一个命令将多个文件加载：  
  
-   所有文件必须都存在于同一目录中。  
  
-   文件必须是文本的所有文件、 所有 gzip 文件或组合文本和 gzip 文件。  
  
-   任何文件可以包含标头信息。  
  
-   所有文件必须都使用相同的字符编码类型。 请参阅 – e 选项。  
  
-   必须将所有文件都加载到同一个表。  
  
-   所有文件将连接在一起并加载，就好像它们是一个文件，并拒绝的行将转到单个拒绝文件。  
  
示例：  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
如果没有加载失败**dwloader**将存储到负载测试和失败描述失败名为的文件中的失败信息的行*load_failure_file_name*。 如果此文件已存在，则 dwloader 将覆盖现有文件。 *load_failure_file_name*第一次失败发生时创建。 如果成功，所有行都加载*load_failure_file_name*未创建。  
  
**-fh** *number_header_rows*  
若要忽略的开头的行 （行） 数*source_data_file_name*。 默认值为 0。  
  
<variable_length_column_options>  
选项*source_data_file_name* ，其字符分隔的可变长度列。 默认情况下， *source_data_file_name*包含可变长度列中的 ASCII 字符。  
  
对于 ASCII 文件，由连续放置分隔符表示 null 值。 例如，在竖线分隔的文件 ("|")，空值将由"| |"。 在以逗号分隔文件中，NULL 将由"（、、"。 此外， **-E** (-emptyStringAsNull) 必须指定选项。 有关详细信息-E，请参阅下面。  
  
**-e** *character_encoding*  
指定的字符编码类型的数据要从数据文件加载。 选项为 ASCII （默认值）、 UTF8、 UTF16，或 UTF16BE，其中 UTF16 是稍有 endian，UTF16BE 是 big-endian。 这些选项是区分大小写。  
  
**-t** *field_delimiter*  
每个字段 （列） 中的行分隔符。 字段分隔符为一个或多个这些 ASCII 转义字符或十六进制 ASCII 值...  
  
|名称|转义字符|十六进制字符|  
|--------|--------------------|-----------------|  
|选项卡|\t|0x09|  
|回车符 (CR)|\r|0x0d|  
|换行符 (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|逗号|','|0x2c|  
|双引号|\\"|0x22|  
|单引号|\\'|0x27|  
  
若要在命令行上指定的管道字符，请将其括用双引号，"|"。 这将由命令行的分析器来避免错误解释。 其他字符都用单引号括起来。  
  
示例：  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t '~|~'  
  
**-r** *row_delimiter*  
源数据文件的每一行分隔符。 行分隔符是一个或多个 ASCII 值。  
  
若要作为分隔符指定回车符 (CR)、 换行符 (LF) 或 tab 字符，可以使用转义字符 （\r、 \n、 \t） 或其十六进制值 （0 x，0 d，09）。 若要指定其他任何特殊字符作为分隔符，请使用其十六进制值。  
  
CR + LF 的示例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的示例：  
  
-r \r  
  
-r 0x0d  
  
LF 的示例：  
  
-r \n  
  
-r 0x0a  
  
需要 for Unix LF。 CR 是必需的 Windows。  
  
**-s** *string_delimiter*  
分隔符字符串数据类型的文本分隔的输入文件的字段。 字符串分隔符是一个或多个 ASCII 值。  它可以被指定为一个字符 (例如，-s *) 还是十六进制值 (例如，-s 0x22 为双引号)。  
  
示例：  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options>  
具有固定长度列的源数据文件有关的选项。 默认情况下， *source_data_file_name*包含可变长度列中的 ASCII 字符。  
  
UTF8 – e 时，不支持固定的宽度列。  
  
**-w** *fixed_width_config_file*  
路径和名称的配置文件的每个列中指定的字符数。 必须指定每个字段。  
  
此文件必须位于加载服务器。 路径可以是 UNC，相对或绝对路径。 中的每一行*fixed_width_config_file*包含该列的名称的一个列和字符数。 每个列，一个行，如下所示，文件中的顺序必须与目标表中的顺序一致：  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
固定宽度配置文件的示例：  
  
SalesCode=3  
  
SalesID=10  
  
示例中的行*source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
在前面的示例中，加载的第一行将具有 SalesCode ="230"和 SalesID = Shirts0056。 第二个加载的行，将有 SalesCode ="320"和 SaleID = Towels1356。  
  
有关如何处理前导空格和尾随空格或数据类型转换在固定的宽度模式下的信息，请参阅[数据类型转换规则 dwloader](dwloader-data-type-conversion-rules.md)。  
  
**-e** *character_encoding*  
指定的字符编码类型的数据要从数据文件加载。 选项为 ASCII （默认值）、 UTF8、 UTF16，或 UTF16BE，其中 UTF16 是稍有 endian，UTF16BE 是 big-endian。 这些选项是区分大小写。  
  
UTF8 – e 时，不支持固定的宽度列。  
  
**-r** *row_delimiter*  
源数据文件的每一行分隔符。 行分隔符是一个或多个 ASCII 值。  
  
若要作为分隔符指定回车符 (CR)、 换行符 (LF) 或 tab 字符，可以使用转义字符 （\r、 \n、 \t） 或其十六进制值 （0 x，0 d，09）。 若要指定其他任何特殊字符作为分隔符，请使用其十六进制值。  
  
CR + LF 的示例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的示例：  
  
-r \r  
  
-r 0x0d  
  
LF 的示例：  
  
-r \n  
  
-r 0x0a  
  
需要 for Unix LF。 CR 是必需的 Windows。  
  
**-D** { **ymd** | ydm | mdy | myd | dmy |dym |*custom_date_format* }  
输入文件中指定的顺序 (m)、 (d)、 年月和日 (y) 对所有 datetime 字段。 默认顺序是 ymd。 若要指定的同一源文件中的多个顺序格式，请使用 – dt 选项。  
  
ymd |dmy  
ydm 和 dmy 允许相同的输入的格式。 两者都允许要需要在开始或结束日期的年份。 例如，对于同时**ydm**和**dmy**日期格式，您可以对 2013年-02-03 或 02-03-2013年输入文件中。  
  
ydm  
你只能加载作为 ydm 格式化为日期时间数据类型和 smalldatetime 的列的输入。 无法将 ydm 值加载到 datetime2、 日期或 datetimeoffset 数据类型的列。  
  
mdy  
mdy 允许<month> <space> <day> <comma> <year>。  
  
Mdy 1975 年 1 月 1，输入数据的示例：  
  
-   1975 年 1 月 1日，  
  
-   75 年 1 月 01 日  
  
-   年 1 月/1/75  
  
-   01011975  
  
myd  
为年 3 月输入文件示例 04,2010: 03-2010年-04 上午，3/2010年/4  
  
dym  
适用于 2010 年 3 月 4 日，输入文件示例： 04-2010年-03，4/2010年/3  
  
*custom_date_format*  
*custom_date_format*是一种自定义日期格式 (例如，MM/dd/yyyy) 和包括的仅向后兼容性。 dwloader 执行不 enfoce 自定义日期格式。 相反，当指定的自定义日期格式， **dwloader**会将它转换到 ymd、 ydm、 mdy、 myd、 dym 或 dmy 的相应设置。  
  
例如，如果指定了 – D MM/dd/yyyy，dwloader 需要所有输入首先，顺序与月的日期一天，然后年份 (mdy)。 它不会强制 2 字符个月，2 数字天，并为指定的自定义日期格式的 4 位数年份。 下面是一些示例日期可进行格式设置输入文件中的日期格式 – D MM/dd/yyyy 时的方式： 01/02/2013，Jan.02.2013，2013 年 1 月 2 日  
  
有关更全面的格式设置信息，请参阅[数据类型转换规则 dwloader](dwloader-data-type-conversion-rules.md)。  
  
**-dt** *datetime_format_file*  
在名为的文件中指定每个日期时间格式*datetime_format_file*。 与不同的命令行参数，包含空格的文件参数不必须括在双引号内。 加载数据时，不能更改日期时间格式。 源数据文件和目标表中的其相应列必须具有相同的格式。  
  
每个行包含目标表和其 datetime 格式的列的名称。  
  
示例：  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
数据库名称将包含临时表。 默认值为-T 选项，这是目标表的数据库与指定的数据库。 有关使用临时数据库的详细信息，请参阅[创建暂存数据库](staging-database.md)。  
  
**-M** *load_mode_option*  
指定是否追加，插入更新，或重新加载数据。 追加是默认模式。  
  
追加  
加载程序在目标表中的现有行的末尾插入行。  
  
fastappend  
加载程序将行插入直接，而无需使用临时表，到目标表中的现有行的末尾。 fastappend 要求多事务 (– m) 选项。 使用 fastappend 时，不能指定一个临时数据库。 没有与 fastappend，这意味着从失败或已中止负载恢复必须由你自己的加载过程回滚。  
  
upsert **-K**  *merge_column* [ ,...*n* ]  
加载程序将使用 SQL Server 合并语句以更新现有行和插入新行。  
  
-K 选项指定的列或列要合并基础。 这些列构成合并键，它应表示唯一行。 如果合并密钥存在目标表中，更新行。 如果合并密钥不存在目标表中，追加行。  
  
对于哈希分布式表，合并密钥必须是或者包含分布列。  
  
对于复制的表，合并密钥是一个或多个列的组合。 根据应用程序的需求指定了这些列。  
  
多个列必须是没有空格、 逗号分隔或逗号分隔的空间并括在单引号中。  
  
如果源表中的两行具有匹配合并密钥值，其各自的行必须相同。  
  
重新加载  
加载程序将它插入的源数据之前截断目标表。  
  
**-b** *batchsize*  
Microsoft 支持部门，建议仅用于*batchsize*是 DMS 执行到计算节点上的 SQL Server 实例大容量复制的 SQL Server 批处理大小。  当*batchsize*指定，则 SQL Server PDW 将重写为每个负载动态计算的批处理负载大小。  
  
从 SQL Server 2012 PDW 开始，控制节点动态计算每个负载的批处理大小默认情况下。 此自动计算基于如内存大小、 目标表类型、 目标表架构、 加载类型、 文件大小和用户的资源类的多个参数。  
  
例如，如果负载模式 FASTAPPEND 并且表具有聚集列存储索引，SQL Server PDW 将按默认尝试使用的批处理大小为 1048576，以便将变得关闭行组和直接加载到列存储而无需通过增量存储。 如果内存不允许批次大小为 1048576，dwloader 将选择较小的 batchsize 创建。  
  
如果负载的类型是 FASTAPPEND， *batchsize*适用于将数据加载到表，否则*batchsize*适用于将数据加载到临时表。  
  
<reject_options>  
指定用于确定加载程序将允许的加载失败的数目的选项。 如果加载失败超出阈值时，加载程序将暂停并提交的任何行。  
  
**-rt** {**值**| 百分比}  
指定是否-*reject_value*中**-rv** *reject_value*选项为文本的行 （值） 或失败 （百分比） 的速率。 默认值为值。  
  
百分比选项是实时计算-rs 选项根据时间间隔发生。  
  
例如，如果加载程序尝试加载 100 行和 25 失败，75 成功，失败率为 25%。  
  
**-rv** *reject_value*  
指定要停止负载前允许的数量或百分比的行的拒绝。 **-Rt**选项确定如果*reject_value*指的行数或行的百分比。  
  
默认值*reject_value*为 0。  
  
当与-rt 值一起使用，加载程序将停止负载，被拒绝的行计数超过 reject_value 时。  
  
当使用-rt 百分比、 加载程序按时间间隔计算百分比 (-rs 选项)。 因此，失败行百分比可能会超过*reject_value*。  
  
**-rs** *reject_sample_size*  
与使用`-rt percentage`选项以指定的增量百分比检查。 例如，如果 reject_sample_size 为 1000年，加载程序将计算失败行百分比后它已尝试加载 1000年行。 它会重新计算失败行百分比后它会尝试加载每个其他的 1000年行。  
  
**-c**  
从左侧和右侧的 char、 nchar、 varchar、 和 nvarchar 字段中移除空白字符。 将转换仅包含空白字符为空字符串的每个字段。  
  
示例：  
  
' 获取截断为 '  
  
'abc' 获取截断为 'abc'  
  
与-E，使用 – c 时 – E 操作先发生。 仅包含空白字符的字段将转换为空字符串，并不为 NULL。  
  
**-E**  
将空字符串转换为 NULL。 默认值是不执行这些转换。  
  
**-m**  
使用多事务模式的第二个阶段的加载;当数据从临时表加载到分布式表。  
  
与**– m**，SQL Server PDW 执行并提交并行的负载。 这比默认加载模式下，更快地执行，但不是事务安全。  
  
而无需**– m**，SQL Server PDW 执行并在每个计算节点中, 分布区同时跨计算节点将按顺序提交加载。 此方法比多事务模式慢，而且是事务安全。  
  
**-m**对于是可选的*追加*，*重新加载*，和*upsert*。  
  
**-m** fastappend 需要。  
  
**-m**不能用于复制的表。  
  
**-m**仅适用于第二个的加载阶段。 它不适用于的第一的加载阶段;正在将数据加载到临时表中。  
  
没有多事务模式中，这意味着从失败或已中止负载恢复必须由你自己的加载过程回滚。  
  
我们建议使用**– m**仅时加载到一个空表，以便你可以恢复的数据丢失。 若要从负载故障中恢复： 删除目标表、 解决负载问题、 重新创建目标表中，和重新运行负载。  
  
**-N**  
验证目标设备具有来自受信任颁发机构的有效 SQL Server PDW 证书。 用于帮助确保你的数据将不会让攻击者截获和发送到未经授权的位置。 证书必须已安装在设备上。 安装证书的唯一受支持的方法是让设备管理员能够使用 Configuration Manager 工具安装它。 如果你不确定设备是否具有安装受信任的证书要求设备管理员。  
  
**-se**  
跳过加载空文件。 这还将跳过解压缩空 gzip 文件。  
  
## <a name="return-code-values"></a>返回代码值  
0 （成功） 或其他整数值 （失败）  
  
在命令窗口或批处理文件中，使用`errorlevel`以显示其返回代码。 例如：  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
使用 PowerShell 时，使用`$LastExitCode`。  
  
## <a name="permissions"></a>权限  
需要负载权限和对目标表的适用权限 (INSERT、 UPDATE、 DELETE)。 将在临时数据库要求 （用于创建临时表） 的创建权限。 如果未使用临时数据库，然后在目标数据库上，则必须创建权限。 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>一般备注  
有关数据类型转换时使用 dwloader 加载的信息，请参阅[数据类型转换规则 dwloader](dwloader-data-type-conversion-rules.md)。  
  
如果参数包含一个或多个空格，则将用双引号的参数。  
  
你应从其安装位置运行加载程序。 可执行 dwloader 预安装与设备和位于 C:\Program Files\Microsoft SQL Server 数据 Warehouse\DWLoader 目录中。  
  
您可以重写参数文件中指定的参数 (-f 选项) 通过指定作为命令行参数。  
  
你可以同时运行加载程序的多个的实例。 加载程序实例的最大数预配置，并且不能更改。 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
加载的数据可能需要更多或更少的源位置中比设备上的空间。 你可以执行测试导入数据来估计磁盘占用量的子集。  
  
尽管**dwloader**是一个事务的过程并将回滚正常失败，不能回滚完成大容量加载已成功完成后返回。 若要取消活动**dwloader**处理、 键入 CTRL + C。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
必须被小于 LOG_SIZE 对于数据库，并且我们建议所有的并发负荷的总大小同时发生的所有加载的总大小为的 LOG_SIZE 小于 50%。 若要实现此大小限制，你可以拆分为多个批次的较大负载。 LOG_SIZE 的详细信息，请参阅[创建数据库](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
在加载时使用一个负载命令的多个文件，所有拒绝的行写入到相同的拒绝文件。 拒绝文件不显示哪些输入的文件包含每个被拒绝的行。  
  
不应作为分隔符的空字符串。 空字符串作为时将使用行分隔符，则加载将失败。 当使用作为列分隔符，负载将忽略分隔符，继续使用默认值"|"作为列分隔符。 当使用作为字符串分隔符，则忽略空字符串并应用默认行为。  
  
## <a name="locking-behavior"></a>锁定行为  
**dwloader**锁定行为会有所不同，具体取决于*load_mode_option*。  
  
-   **追加**– 追加是建议的最常见的选项。 将数据加载追加到临时表。 下面将详细描述了锁定。  
  
-   **快速追加**– 快速追加加载直接到最终表采用 ExclusiveUpdate 表锁，并为不使用临时表的唯一模式。  
  
-   **重新加载**– 重新加载将数据加载到临时表和需要的临时表和最终的表的排他锁。 并发操作不建议重新加载。  
  
-   **upsert** – Upsert 将数据加载到临时表，然后执行合并操作从临时表到最终表。 Upsert 不需要最终的表上的排他锁。 使用 upsert 时，性能可能会不同。 在你的环境中测试行为。  
  
### <a name="locking-behavior"></a>锁定行为  
**追加模式锁定**  
  
追加可以以多事务 （使用 – m 自变量） 的模式运行，但它不是事务安全。 因此追加 （不使用 – m 自变量） 用作事务操作。 遗憾的是，在最终 INSERT SELECT 操作时，事务模式低于当前大约六倍多事务模式。  
  
追加模式将数据加载在两个阶段。 第一阶段将数据从原始文件加载到临时表同时 （碎片可以发生）。 第二个阶段将数据从临时表加载到最终表。 第二个阶段执行**INSERT INTO...选择 WITH (TABLOCK)**操作。 下表显示的锁定行为对最终的目录，并使用时的日志记录行为追加模式：  
  
|表类型|多事务<br />模式 (-m)|表为空|支持的并发|日志记录|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|堆|是|用户帐户控制|是|最小|  
|堆|是|“否”|是|最小|  
|堆|否|是|否|最小|  
|堆|否|“否”|否|最小|  
|Cl|是|用户帐户控制|否|最小|  
|Cl|是|“否”|是|“完全”|  
|Cl|否|是|否|最小|  
|Cl|否|“否”|是|“完全”|  
  
上面的表所示**dwloader**使用追加模式加载到堆或聚集的索引 (CI) 表，或如果没有多事务的标志，以及将加载到一个空表或非空表。 表中会显示锁定和日志记录的每个此类组合的负载的行为。 例如，加载 （第 2 个） 阶段，并带有追加模式到多事务模式下没有聚集索引和一个空表将具有 PDW 的表上创建的排他锁和日志记录是最小。 这意味着客户将无法加载同时到一个空表的 （第二个） 的阶段和查询。 但是，在加载时用到非空表相同的配置，PDW 将不会发出对表的排他锁并且可能并发。 遗憾的是，完整的日志记录会发生，减慢了处理过程。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-dwloader-example"></a>A. 简单 dwloader 示例  
下面的示例演示启动的**加载程序**与仅选择所需的选项。 其他选项会从全局配置文件中， *loadparamfile.txt*。  
  
使用 SQL Server 身份验证的示例。  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
相同的示例中使用 Windows 身份验证。  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
使用源文件和错误文件的自变量的示例。  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. 将数据加载到 AdventureWorks 表  
下面的示例是将数据加载到一个批处理脚本的一部分**AdventureWorksPDW2012**。  若要查看完整的脚本，请打开附带的 aw_create.bat 文件**AdventureWorksPDW2012**安装包。 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

以下脚本代码段使用 dwloader 数据加载到 DimAccount 和 DimCurrency 表。 此脚本使用以太网地址。 如果它已使用 InfiniBand，服务器将*< appliance_name >*`-SQLCTL01`。  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
下面是用于 DimAccount 表的 DDL。  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
下面是数据文件，DimAccount.txt，包含要加载到表 DimAccount 数据的示例。  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. 从命令行中加载数据  
示例 B 中的脚本可以替换为在命令行中，输入所有参数，如下面的示例中所示。  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe –S <Control node IP> -E –M reload –e UTF16 -i .\DimAccount.txt –T AdventureWorksPDW2012.dbo.DimAccount –R DimAccount.bad –t "|" –r \r\n –U <login> -P <password>  
```  
  
命令行参数的说明：  
  
-   *C:\Program Files\Microsoft SQL Server 并行数据 Warehouse\100\dwloader.exe*是 dwloader.exe 的安装的位置。  
  
-   *-S*跟控制节点的 IP 地址。  
  
-   *-E*指定加载为 NULL 的空字符串。  
  
-   *-M 重新加载*指定之前它将源数据截断目标表。  
  
-   *-e UTF16*指示源文件使用小 endian 字符编码类型。  
  
-   *-i.\DimAccount.txt*指定数据是在名为 DimAccount.txt 已存在于当前目录。  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount*指定要接收数据的表的第 3 部分名称。  
  
-   *-R DimAccount.bad*指定加载失败的行将写入到名为 DimAccount.bad 的文件。  
  
-   *– t"|"*指示用管道字符分隔的输入文件 DimAccount.txt 中的字段。  
  
-   *-r \r\n*指定 DimAccount.txt 中的每一行结尾回车符和换行符。  
  
-   *-U < >-P login_name <password>* 指定登录名和有权执行加载的登录名的密码。  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
