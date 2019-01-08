---
title: bcp 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1ba79898fe1f218e51b8eda10f2fb91784a8d7e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757349"
---
# <a name="bcp-utility"></a>bcp 实用工具
  **Bcp**大容量复制数据的实例之间[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和用户指定格式的数据文件。 使用 **bcp** 实用工具可以将大量新行导入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表，或将表数据导出到数据文件。 除非与 **queryout** 选项一起使用，否则使用该实用工具不需要了解 [!INCLUDE[tsql](../includes/tsql-md.md)]知识。 若要将数据导入表中，必须使用为该表创建的格式文件，或者必须了解表的结构以及对于该表中的列有效的数据类型。  
  
 ![主题链接图标](../../2014/database-engine/media/topic-link.gif "主题链接图标")有关 bcp 语法中使用的语法约定，请参阅 [Transact-SQL 语法约定 (Transact-SQL)](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)。  
  
> [!NOTE]  
>  如果使用 **bcp** 备份数据，请创建一个格式化文件来记录数据格式。 **bcp** 数据文件不包括任何架构或格式信息，因此如果已删除表或视图并且不具备格式化文件，则可能无法导入数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
   bcp [database_name.] schema.{table_name | view_name | "query" {indata_file | outdata_file | queryoutdata_file | format nul}  
  
[-apacket_size]  
[-bbatch_size]  
[-c]  
[-C { ACP | OEM | RAW | code_page } ]  
[-ddatabase_name]  
[-eerr_file]  
[-E]  
[-fformat_file]  
[-Ffirst_row]  
[-h"hint [,...n]"]   
[-iinput_file]  
[-k]  
[-Kapplication_intent]  
[-Llast_row]  
[-mmax_errors]  
[-n]  
[-N]  
[-ooutput_file]  
[-Ppassword]  
[-q]  
[-rrow_term]  
[-R]  
[-S [server_name[\instance_name]]  
[-tfield_term]  
[-T]  
[-Ulogin_id]  
[-v]  
[-V (80 | 90 | 100 | 110)]  
[-w]  
[-x]  
/?  
```  
  
## <a name="arguments"></a>参数  
 *data_file*  
 数据文件的完整路径。 将数据批量导入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]时，数据文件将包含要复制到指定的表或视图中的数据。 从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中批量导出数据时，数据文件将包含从表或视图中复制的数据。 路径可以有 1 到 255 个字符。 数据文件最多可包含 2<sup>63</sup> - 1 行。  
  
 *database_name*  
 指定的表或视图所在数据库的名称。 如果未指定，则使用用户的默认数据库。  
  
 也可以使用 `d-` 显式指定数据库名称。  
  
 **in** *data_file* | **out**_data_file_ | **queryout**_data_file_ | **format nul**  
 指定大容量复制的方向，具体如下：  
  
-   **in** 从文件复制到数据库表或视图。  
  
-   **out** 从数据库表或视图复制到文件。 如果指定了现有文件，则该文件将被覆盖。 提取数据时，请注意 **bcp** 实用工具将空字符串表示为 null，而将 null 字符串表示为空字符串。  
  
-   **queryout** 从查询中复制，仅当从查询大容量复制数据时才必须指定此选项。  
  
-   **格式**创建格式化文件基于指定的选项 (**-n**， `-c`， `-w`，或 **-N**) 以及表或视图的分隔符。 大容量复制数据时， **bcp** 命令可以引用一个格式化文件，从而避免以交互方式重复输入格式信息。 **format** 选项要求指定 **-f** 选项；创建 XML 格式化文件时还需要指定 **-x** 选项。 有关详细信息，请参阅 [创建格式化文件 (SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)。 必须将 **nul** 指定为值 (**format nul**)。  
  
 *所有者*  
 表或视图的所有者的名称。 如果执行该操作的用户拥有指定的表或视图，则*owner* 是可选的。 如果未指定 *owner*，并且执行该操作的用户不是指定的表或视图的所有者，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将返回错误消息，而且该操作将取消。  
  
 **"** *query* **"**  
 一个返回结果集的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询。 如果该查询返回多个结果集，则只将第一个结果集复制到数据文件，而忽略其余的结果集。 将查询用双引号括起来，将查询中嵌入的任何内容用单引号括起来。 从查询大容量复制数据时，也必须指定**queryout** 。  
  
 只要在执行 bcp 语句之前存储过程内引用的所有表均存在，查询就可以引用该存储过程。 例如，如果存储过程生成一个临时表，则 **bcp** 语句便会失败，因为该临时表只在运行时可用，而在语句执行时不可用。 在这种情况下，应考虑将存储过程的结果插入表中，然后使用 **bcp** 将数据从表复制到数据文件中。  
  
 *table_name*  
 将数据导入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) 时为目标表名称，将数据从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导出时 (**out**) 为源表名称。  
  
 view_name  
 将数据复制到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) 时为目标视图名称，从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中复制数据时 (**out**) 为源视图名称。 只有其中所有列都引用同一个表的视图才能用作目标视图。 有关将数据复制到视图的限制的详细信息，请参阅[《INSERT &#40;Transact-SQL&#41;》](/sql/t-sql/statements/insert-transact-sql)。  
  
 **-a** *packet_size*  
 指定服务器发出或接收的每个网络数据包的字节数。 可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] （或 **sp_configure** 系统存储过程）来设置服务器配置选项。 但是，可以使用此选项逐个替代服务器配置选项。 *packet_size* 的取值范围为 4096 到 65535 字节，默认为 4096 字节。  
  
 增大数据包可以提高大容量复制操作的性能。 如果无法得到请求的较大数据包，则使用默认值。 **bcp** 实用工具生成的性能统计信息可以显示所用的数据包大小。  
  
 **-b** *batch_size*  
 指定每批导入数据的行数。 每个批次均作为一个单独的事务进行导入并记录，在提交之前会导入整批。 默认情况下，数据文件中的所有行均作为一个批次导入。 若要将行分为多个批次进行操作，请指定小于数据文件中的行数的 *batch_size* 。 如果任何批次的事务失败，则将只回滚当前批次中的插入。 已经由已提交事务导入的批次不会受到将来失败的影响。  
  
 不使用此选项结合 **-h"** ROWS_PER_BATCH  **= *`bb`*"** 选项。  
  
 `-c`  
 使用字符数据类型执行该操作。 此选项不提示输入每个字段;它使用`char`作为存储类型，不带前缀; 使用**\t** （制表符） 作为字段分隔符以及**\r\n** （换行符） 作为行终止符。 `-c` 与 `-w` 不兼容。  
  
 有关详细信息，请参阅[使用字符格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)。  
  
 **-C** { **ACP** | **OEM** | **RAW** | *code_page* }  
 指定该数据文件中数据的代码页。 *code_page*仅当数据含有相关`char`， `varchar`，或`text`字符值大于 127 或小于 32 列。  
  
> [!NOTE]  
>  建议在格式化文件中为每个列指定一个排序规则名称。  
  
|代码页值|Description|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252)。|  
|OEM|客户端使用的默认代码页。 未指定 **-C** 时使用的默认代码页。|  
|RAW|不进行代码页间的转换。 因为不进行转换，所以这是最快的选项。|  
|*code_page*|特定的代码页编号，例如 850。<br /><br /> **\*\* 重要\* \***  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不支持代码页 65001(utf-8 编码）。|  
  
 `-d` *database_name*  
 指定要连接到的数据库。 默认情况下，bcp.exe 连接到用户的默认数据库。 如果`-d` *database_name*和三个部分构成的名称 (*database_name.schema.table*，作为第一个参数传递给 bcp.exe) 指定，将发生错误，因为不能指定两次数据库名称。如果*database_name*开始使用连字符 （-） 或正斜杠 （/），不要添加之间有空格`-d`和数据库名称。  
  
 **-e** *err_file*  
 指定错误文件的完整路径，此文件用于存储 **bcp** 实用工具无法从文件传输到数据库的所有行。 **bcp** 命令产生的错误消息将被发送到用户的工作站。 如果不使用此选项，则不会创建错误文件。  
  
 如果 *err_file* 以连字符 (-) 或正斜杠 (/) 开头，则不要在 **-e** 与 *err_file* 值之间包含空格。  
  
 **-E**  
 指定导入数据文件中的标识值用于标识列。 如果未指定 **-E** ，则将忽略要导入的数据文件中此列的标识值，而且 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将根据创建表期间指定的种子值和增量值自动分配唯一值。  
  
 如果数据文件不包含表或视图中的标识列的值，则可使用格式化文件指定，在导入数据时应跳过表或视图中的标识列；[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将自动为该列分配唯一值。 有关详细信息，请参阅 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)。  
  
 **-E** 选项有一个特殊的权限要求。 有关详细信息，请参阅本主题后面的“备注”。  
  
 **-f** *format_file*  
 指定格式化文件的完整路径。 此选项的含义取决于使用它的环境，具体如下：  
  
-   如果 **-f** 与 **format** 选项一起使用，则将为指定的表或视图创建指定的 *format_file* 。 若要创建 XML 格式化文件，请同时指定 **-x** 选项。 有关详细信息，请参阅 [创建格式化文件 (SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)。  
  
-   如果与 **in** 或 **out** 选项一起使用，则 **-f** 需要一个现有的格式化文件。  
  
    > [!NOTE]  
    >  与 **in** 或 **out** 选项一起使用时，格式化文件是可选的。 如果没有 **-f**选项时，如果 **-n**， `-c`， `-w`，或者 **-N**未指定，则该命令将提示输入格式信息，并允许您保存做的响应的格式化文件 （默认文件名为 Bcp.fmt）。  
  
 如果 *format_file* 以连字符 (-) 或正斜杠 (/) 开头，则不要在 **-f** 与 *format_file* 值之间包含空格。  
  
 **-F** *first_row*  
 指定要从表中导出或从数据文件导入的第一行的编号。 此参数需要大于 (>) 0 的值但小于 (\<) 或总的行数等于 （=）。 如果未指定此参数，则默认为文件的第一行。  
  
 *first_row* 可以是一个最大为 2^63-1 的正整数值。 **-F**_first_row_ 的值从 1 开始。  
  
 **-h"** *hint*[ **,**... *n*] **"**  
 指定向表或视图中大容量导入数据时要用到的提示。  
  
 ORDER **(**_column_[ASC | DESC] [**,**...*n*]**)**  
 数据文件中的数据排序次序。 如果根据表中的聚集索引（如果有）对要导入的数据排序，则可提高批量导入的性能。 如果数据文件以不同的次序（即不同于聚集索引键的次序）排序，或者表中不存在任何聚集索引，则将忽略 ORDER 子句。 提供的列名必须是目标表中有效的列名。 默认情况下， **bcp** 假定数据文件没有排序。 对于经过优化的大容量导入， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 还将验证导入的数据是否已排序。  
  
 ROWS_PER_BATCH **=**_bb_  
 每批数据的行数（即 *bb*）。 在未指定 **-b** 时使用，这将导致整个数据文件作为单个事务发送到服务器。 服务器根据 *bb*值优化大容量加载。 默认情况下，ROWS_PER_BATCH 是未知的。  
  
 KILOBYTES_PER_BATCH **=** *cc*  
 每批的以千字节计数的近似数据量（即 *cc*）。 默认情况下，KILOBYTES_PER_BATCH 是未知的。  
  
 TABLOCK  
 指定在大容量加载操作期间获取大容量更新表级别的锁；否则，获取行级别的锁。 由于在大容量复制操作期间拥有锁可以减少表中的锁争夺，所以此提示可显著提高性能。 如果表没有索引并且指定了 **TABLOCK** ，则该表可以同时由多个客户端加载。 默认情况下，锁定行为由表选项 **table lock on bulk load**决定。  
  
 CHECK_CONSTRAINTS  
 指定在批量导入操作期间，必须检查所有对目标表或视图的约束。 如果没有 CHECK_CONSTRAINTS 提示，则忽略所有 CHECK 和 FOREIGN KEY 约束；操作完成后，对表的约束将被标记为不可信。  
  
> [!NOTE]  
>  始终强制使用 UNIQUE、PRIMARY KEY 和 NOT NULL 约束。  
  
 在某些时候，需要检查整个表的约束。 如果在批量导入操作之前表为非空状态，则重新验证约束的开销可能超过将 CHECK 约束应用于增量数据的开销。 因此，建议您在正常情况下，在进行增量式批量导入时启用约束检查。  
  
 当输入数据包含违反约束的行时，您可能希望禁用约束（默认行为）。 如果禁用 CHECK 约束，您可以导入数据，然后使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句删除无效数据。  
  
> [!NOTE]  
>  **bcp** 现在会强制执行数据验证和数据检查，这样，在对数据文件中的无效数据执行脚本时，可能会导致脚本失败。  
  
> [!NOTE]  
>  **-m** *max_errors* 开关不适用于约束检查。  
  
 FIRE_TRIGGERS  
 与 **in** 参数一同指定，在目标表中定义的任何插入触发器都将在大容量复制操作期间运行。 如果未指定 FIRE_TRIGGERS，将不运行任何插入触发器。 对于 **out**、**queryout** 和 **format** 参数，将忽略 FIRE_TRIGGERS。  
  
 **-i** *input_file*  
 指定包含每个数据字段的命令提示问题的响应，使用交互模式下执行大容量复制时的响应文件的名称 (**-n**， `-c`， `-w`，或 **-N**未指定)。  
  
 如果 *input_file* 以连字符 (-) 或正斜杠 (/) 开头，则不要在 **-i** 与 *input_file* 值之间包含空格。  
  
 **-k**  
 指定在操作过程中空列应该保留 null 值，而不是所插入列的任何默认值。 有关详细信息，请参阅[在批量导入期间保留 Null 或使用默认值 (SQL Server)](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)。  
  
 **-K** *application_intent*  
 连接到服务器时声明应用程序工作负荷类型。 唯一可能的值是 **ReadOnly**。 如果未指定 **-K**，bcp 实用工具将不支持连接到 AlwaysOn 可用性组中的次要副本。 有关详细信息，请参阅[活动次要副本：可读辅助副本 （AlwaysOn 可用性组）](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 **-L** *last_row*  
 指定要从表中导出或从数据文件中导入的最后一行的编号。 此参数需要大于 (>) 0 的值但小于 (\<) 或最后一行的行数等于 （=）。 如果未指定此参数，则默认为文件的最后一行。  
  
 *last_row* 可以是一个最大为 2^63-1 的正整数值。  
  
 **-m** *max_errors*  
 指定取消 **bcp** 操作之前可能出现的语法错误的最大数目。 语法错误是指将数据转换为目标数据类型时的错误。 *max_errors* 总数不包括只能在服务器中检测到的错误，如约束冲突。  
  
 无法由 **bcp** 实用工具复制的行将被忽略，并计为一个错误。 如果未包括此选项，则默认值为 10。  
  
> [!NOTE]  
>  **-M**选项也不适用于转换`money`或`bigint`数据类型。  
  
 **-n**  
 使用数据的本机（数据库）数据类型执行大容量复制操作。 此选项不提示输入每个字段，它将使用本机值。  
  
 有关详细信息，请参阅[使用本机格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)。  
  
 **-N**  
 执行大容量复制操作时，对非字符数据使用本机（数据库）数据类型的数据，对字符数据使用 Unicode 字符。 此选项是 `-w` 选项的一个替代选项，并具有更高的性能。此选项主要用于通过数据文件将数据从一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例传送到另一个实例。 此选项不提示输入每个字段。 如果要传送包含 ANSI 扩展字符的数据，并希望利用本机模式的性能优势，则可使用此选项。  
  
 有关详细信息信息，请参阅 [使用 Unicode 本机格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)。  
  
 如果导出，然后使用数据导入到同一表架构与 bcp.exe **-N**，可能会显示截断警告，则在存在固定的长度的非 Unicode 字符列 (例如， `char(10)`)。  
  
 可忽略该警告。 解决此警告的一个方法是使用 **-n** 来替代 **-N**。  
  
 **-o** *output_file*  
 指定文件名称，该文件用于接收从命令提示符重定向来的输出。  
  
 如果 *output_file* 以连字符 (-) 或正斜杠 (/) 开头，则不要在 **-o** 与 *output_file* 值之间包含空格。  
  
 **-P** *password*  
 指定登录 ID 的密码。 如果未使用此选项， **bcp** 命令将提示输入密码。 如果在命令提示符的末尾使用此选项，但不提供密码，则 **bcp** 将使用默认密码 (NULL)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]  
  
 若要屏蔽密码，请不要指定 **-P** 选项和 **-U** 选项。 而应在指定 **bcp** 以及 **-U** 选项和其他开关（不指定 **-P**）之后按 Enter，这时命令会提示输入密码。 这种方法可以确保输入密码时对其屏蔽。  
  
 如果 password 以连字符 (-) 或正斜杠 (/) 开头，则不要在 **-P** 与 password 值之间添加空格。  
  
 `-q`  
 在 **bcp** 实用工具和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例之间的连接中，执行 SET QUOTED_IDENTIFIERS ON 语句。 使用此选项可以指定包含空格或单引号的数据库、所有者、表或视图的名称。 将由三部分组成的整个表名或视图名用英文双引号 ("") 引起来。  
  
 必须使用 -q 选项，才能指定包含空格或单引号的数据库名称。  
  
 `-q` 不适用于传递到 `-d` 的值。  
  
 有关详细信息，请参阅本主题后面的“备注”。  
  
 **-r** *row_term*  
 指定行终止符。 默认的行终止符是 **\n** （换行符）。 使用此参数可替代默认行终止符。 有关详细信息，请参阅 [指定字段终止符和行终止符 (SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)。  
  
 如果您在 bcp.exe 命令中以十六进制表示法指定行终止符，则该值将在 0x00 处截断。 例如，如果您指定 0x410041，则将使用 0x41。  
  
 如果 *row_term* 以连字符 (-) 或正斜杠 (/) 开头，则不要在 **-r** 与 *row_term* 值之间包含空格。  
  
 **-R**  
 指定使用客户端计算机区域设置中定义的区域格式，将货币、日期和时间数据大容量复制到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中。 默认情况下，将忽略区域设置。  
  
 **-S** *server_name*[ **\\**_instance_name_]  
 指定要连接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。 如果未指定服务器，则 **bcp** 实用工具将连接到本地计算机上的默认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。 如果从网络或本地命名实例上的远程计算机中运行 **bcp** 命令，则必须使用此选项。 若要连接到服务器上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 默认实例，请仅指定 *server_name*。 若要连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的命名实例，请指定 *server_name**_\\_** instance_name*。  
  
 `-t` *field_term*  
 指定字段终止符。 默认的字段终止符是 **\t** （制表符）。 使用此参数可以替代默认字段终止符。 有关详细信息，请参阅 [指定字段终止符和行终止符 (SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)。  
  
 如果您在 bcp.exe 命令中以十六进制表示法指定字段终止符，则该值将在 0x00 处截断。 例如，如果您指定 0x410041，则将使用 0x41。  
  
 如果*field_term*开始使用连字符 （-） 或正斜杠 （/），不包括之间有空格`-t`并且*field_term*值。  
  
 **-T**  
 指定 **bcp** 实用工具通过使用集成安全性的受信任连接连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 不需要网络用户的安全凭据 login_id 和 password。 如果未指定 **-T** ，则需要指定 **-U** 和 **-P** 才能成功登录。  
  
 **-U** *login_id*  
 指定用于连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的登录 ID。  
  
> [!IMPORTANT]  
>  如果 **bcp** 实用工具通过使用集成安全性的可信连接连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，则使用的是 **-T** 选项（可信连接），而不是用户名和密码的组合。  
  
 **-v**  
 报告 **bcp** 实用工具的版本号和版权信息。  
  
 **-V** (**80** | **90** | **100**| **110**)  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]早期版本中的数据类型执行大容量复制操作。 此选项并不提示输入每个字段，它将使用默认值。  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110 = [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]**  
  
 例如，若要为 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]不支持、但是在较高版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中引入的类型生成数据，请使用 -V80 选项。  
  
 有关详细信息，请参阅 [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
  
 `-w`  
 使用 Unicode 字符执行大容量复制操作。 此选项不提示输入每个字段;它使用`nchar`作为存储类型，不带前缀**\t** （制表符） 作为字段分隔符，和**\n** （换行符） 作为行终止符。 `-w` 与 `-c` 不兼容。  
  
 有关详细信息，请参阅 [使用 Unicode 字符格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)。  
  
 **-x**  
 与 **format** 和 **-f**_format_file_ 选项一起使用，可生成基于 XML 的格式化文件，而不是默认的非 XML 格式化文件。 在导入或导出数据时，**-x** 不起作用。 如果不与 **format** 和 **-f**_format_file_ 一起使用，则将生成错误。  
  
## <a name="remarks"></a>备注  
 **Bcp** 12.0 客户端安装在安装时[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]工具。 如果同时安装了 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 和早期版本 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的工具，使用的可能是早期版本的 **bcp** 客户端，而不是 **bcp** 12.0 客户端，具体情况取决于 PATH 环境变量的值。 此环境变量定义 Windows 用于搜索可执行文件的目录集。 若要确定当前所使用的版本，请在 Windows 命令提示符下运行 **bcp /v** 命令。 有关如何在 PATH 环境变量中设置命令路径的信息，请参阅 Windows 帮助。  
  
 只有当 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 一起安装后，才支持 XML 格式化文件。  
  
 有关在何处查找或如何运行 **bcp** 实用工具的信息以及有关命令提示实用工具语法约定的信息，请参阅[《Command Prompt Utility Reference &#40;Database Engine&#41;》](../tools/command-prompt-utility-reference-database-engine.md)（命令提示实用工具参考（数据库引擎））。  
  
 有关准备数据以进行批量导入或导出操作的信息，请参阅[准备用于批量导出或导入的数据 (SQL Server)](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)。  
  
 有关何时在事务日志中记录由批量导入执行的行插入操作的信息，请参阅 [《Prerequisites for Minimal Logging in Bulk Import》](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)（批量导入的最小日志记录的先决条件）。  
  
## <a name="native-data-file-support"></a>本机数据文件支持  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中， **bcp** 实用工具支持与 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]、 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]和 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]兼容的本机数据文件。  
  
## <a name="computed-columns-and-timestamp-columns"></a>计算列和 timestamp 列  
 为计算列或 `timestamp` 列导入的数据文件中的值将被忽略，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将自动分配值。 如果数据文件不包含表中的计算列或 `timestamp` 列的值，则可使用格式化文件指定应在导入数据时忽略表中的计算列或 `timestamp` 列；[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将自动为列分配值。  
  
 计算列和 `timestamp` 列会照常从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 大容量复制到数据文件中。  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>指定包含空格或引号的标识符  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 标识符可以包含嵌入的空格和引号等字符。 此类标识符必须按以下方式处理：  
  
-   如果在命令指示符处指定的标识符或文件名包含空格或引号，则需用英文双引号 ("") 将该标识符引起来。  
  
     例如，下面的 `bcp out` 命令创建了一个名为 `Currency Types.dat`的数据文件：  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   若要指定包含空格或引号的数据库名称，必须使用 `-q` 选项。  
  
-   对于包含嵌入空格或引号的所有者、表或视图的名称，可以执行以下任一操作：  
  
    -   指定 `-q` 选项，或者  
  
    -   将所有者、表或视图的名称括在方括号 ([]) 中，并用引号引起来。  
  
## <a name="data-validation"></a>数据验证  
 **bcp** 现在会强制执行数据验证和数据检查，这样，在对数据文件中的无效数据执行脚本时，可能会导致脚本失败。 例如， **bcp** 现在可以验证：  
  
-   `float` 或 `real` 数据类型的本机表示形式是否有效。  
  
-   Unicode 数据的字节数是否为偶数。  
  
 可以在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中批量导入的无效数据类型现在可能无法加载。在早期版本中，仅当客户端尝试访问无效数据时才出现失败。 在大容量加载后查询数据时，添加的验证可最大限度地减少警告。  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>批量导出或导入 SQLXML 文档  
 若要批量导出或导入 SQLXML 数据，请在格式化文件中使用下列数据类型之一。  
  
|数据类型|效果|  
|---------------|------------|  
|SQLCHAR 或 SQLVARYCHAR|在客户端代码页或排序规则隐含的代码页中发送数据。 与在不指定格式化文件的情况下指定 `-c` 开关具有相同的效果。|  
|SQLNCHAR 或 SQLNVARCHAR|以 Unicode 格式发送数据。 与在不指定格式化文件的情况下指定 `-w` 开关具有相同的效果。|  
|SQLBINARY 或 SQLVARYBIN|不经任何转换即发送数据。|  
  
## <a name="permissions"></a>权限  
 **bcpout** 操作要求对源表有 SELECT 权限。  
  
 **bcpin** 操作要求至少对目标表有 SELECT/INSERT 权限。 此外，如果下列任一条件成立，则要求拥有 ALTER TABLE 权限：  
  
-   存在约束，但没有指定 CHECK_CONSTRAINTS 提示。  
  
    > [!NOTE]  
    >  禁用约束是默认行为。 若要显式启用约束，请使用 **-h** 选项和 CHECK_CONSTRAINTS 提示。  
  
-   存在触发器，但没有指定 FIRE_TRIGGER 提示。  
  
    > [!NOTE]  
    >  默认情况下，不激发触发器。 若要显式激发触发器，请使用 **-h** 选项和 FIRE_TRIGGERS 提示。  
  
-   可以使用 **-E** 选项从数据文件导入标识值。  
  
> [!NOTE]  
>  要求对目标表具有 ALTER TABLE 权限是 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]的新要求。 如果用户帐户不具有对目标表的 ALTER TABLE 权限，这项新要求有可能导致不强制使用触发器和约束检查的 **bcp** 脚本失败。  
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>字符模式 (-c) 和本机模式 (-n) 最佳做法  
 本节提供与字符模式 (-c) 和本机模式 (-n) 有关的一些建议。  
  
-   （管理员/用户）应尽可能使用本机格式 (-n) 以避免分隔符问题。 使用本机格式可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]进行导出和导入。 如果数据将导入到非 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，则使用 -c 或 -w 选项从[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导出数据。  
  
-   （管理员）在使用 BCP OUT 时验证数据。 例如，在您使用 BCP OUT、BCP IN，然后又使用 BCP OUT 时，请验证数据正确导出，并且终止符值未用作某个数据值的一部分。 请考虑使用随机的十六进制值覆盖默认的终止符（使用 -t 和 -r 选项），以便避免终止符值和数据值之间的冲突。  
  
-   （用户）使用长且唯一的终止符（任意字节或字符序列）可以最大程度减少与实际字符串值冲突的可能性。 这可以通过使用 -t 和 -r 选项实现。  
  
## <a name="examples"></a>示例  
 本部分包含以下示例：  
  
-   A. 将表行复制到数据文件中（使用可信连接）  
  
-   B. 将表行复制到数据文件中（使用混合模式身份验证）  
  
-   C. 将文件中的数据复制到表中  
  
-   D. 将特定的列复制到数据文件中  
  
-   E. 将特定的行复制到数据文件中  
  
-   F. 将查询中的数据复制到数据文件中  
  
-   G. 创建非 XML 格式化文件  
  
-   H. 创建 XML 格式化文件  
  
-   I. 使用格式化文件进行 **bcp**批量导入  
  
### <a name="a-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>A. 将表行复制到数据文件中（使用可信连接）  
 以下示例阐释了 **表中的** out `AdventureWorks2012.Sales.Currency` 选项。 此示例创建一个名为 `Currency.dat` 的数据文件，并使用字符格式将表数据复制到该文件中。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 在命令提示符处输入以下命令：  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -T -c  
```  
  
### <a name="b-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>B. 将表行复制到数据文件中（使用混合模式身份验证）  
 以下示例阐释了 **表中的** out `AdventureWorks2012.Sales.Currency` 选项。 此示例创建一个名为 `Currency.dat` 的数据文件，并使用字符格式将表数据复制到该文件中。  
  
 该示例假定你使用混合模式身份验证，必须使用 **-U** 开关指定登录 ID。 并且，除非你连接到本地计算机上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的默认实例，否则请使用 **-S** 开关指定系统名称和实例名称（可选）。  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -c -U<login_id> -S<server_name\instance_name>  
```  
  
 系统将提示您输入密码。  
  
### <a name="c-copying-data-from-a-file-to-a-table"></a>C. 将文件中的数据复制到表中  
 以下示例使用上一个示例中创建的文件 (`Currency.dat`) 来阐释 **in** 选项。 但是，此示例将首先创建一个 `AdventureWorks2012 Sales.Currency` 表的空副本 `Sales.Currency2`，数据将被复制到该副本中。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 若要创建空表，可在查询编辑器中输入以下命令：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO AdventureWorks2012.Sales.Currency2   
FROM AdventureWorks2012.Sales.Currency WHERE 1=2;  
```  
  
 若要将字符数据大容量复制到新表中（即导入数据），可在命令提示符处输入以下命令：  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -c  
```  
  
 若要验证命令是否成功，并在查询编辑器中显示表的内容，请输入：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM Sales.Currency2  
```  
  
### <a name="d-copying-a-specific-column-into-a-data-file"></a>D. 将特定的列复制到数据文件中  
 若要复制特定列，可以使用 **queryout** 选项。 下面的示例仅将 `Name` 表中的 `Sales.Currency` 列复制到数据文件中。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp "SELECT Name FROM AdventureWorks.Sales.Currency" queryout Currency.Name.dat -T -c  
```  
  
### <a name="e-copying-a-specific-row-into-a-data-file"></a>E. 将特定的行复制到数据文件中  
 若要复制特定行，可以使用 **queryout** 选项。 下面的示例仅将名为 `Jarrod Rana` 的联系人的行从表 `AdventureWorks2012.Person.Person` 复制到数据文件 (`Jarrod Rana.dat`) 中。该示例假定你使用的是 Windows 身份验证，并且与运行 **bcp** 命令的服务器实例之间具有可信连接。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp "SELECT * FROM AdventureWorks2012.Person.Person WHERE FirstName='Jarrod' AND LastName='Rana' "  queryout "Jarrod Rana.dat" -T -c  
```  
  
### <a name="f-copying-data-from-a-query-to-a-data-file"></a>F. 将查询中的数据复制到数据文件中  
 若要将 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句的结果集复制到数据文件中，请使用 **queryout** 选项。 下面的示例将 `AdventureWorks2012.Person.Person` 表中的姓名复制到 `Contacts.txt` 数据文件中；这些姓名先按姓排序，再按名排序。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp "SELECT FirstName, LastName FROM AdventureWorks2012.Person.Person ORDER BY LastName, Firstname" queryout Contacts.txt -c -T  
```  
  
### <a name="g-creating-a-non-xml-format-file"></a>G. 创建非 XML 格式化文件  
 下面的示例为 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中的 `Currency.fmt` 表创建一个非 XML 格式化文件 `Sales.Currency`。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c  -f Currency.fmt  
```  
  
 有关详细信息，请参阅 [非 XML 格式化文件 (SQL Server)](../relational-databases/import-export/xml-format-files-sql-server.md)早期版本支持的原始格式。  
  
### <a name="h-creating-an-xml-format-file"></a>H. 创建 XML 格式化文件  
 下面的示例为 `Currency.xml` 数据库中的 `Sales.Currency` 表创建一个名为 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 的 XML 格式化文件。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c -x -f Currency.xml  
```  
  
> [!NOTE]  
>  若要使用 **-x** 开关，则必须使用 **bcp** 9.0 客户端。 有关如何使用 **bcp** 9.0 客户端的信息，请参阅“备注”。  
  
 有关详细信息，请参阅 [XML 格式化文件 (SQL Server)](../relational-databases/import-export/xml-format-files-sql-server.md)。  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. 使用格式化文件进行 bcp 批量导入  
 向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的实例中导入数据时，若要使用以前创建的格式化文件，请同时使用 **-f** 开关和 **in** 选项。 例如，以下命令通过使用以前创建的格式化文件 (`Currency.dat`)，将数据文件 `Sales.Currency` 的内容大容量复制到 `Sales.Currency2` 表的副本 (`Currency.xml`) 中。 该示例假定你使用 Windows 身份验证，并且与运行 **bcp** 命令所针对的服务器实例之间具有可信连接。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -f Currency.xml  
```  
  
> [!NOTE]  
>  如果数据文件字段和表中的列不同（例如，在编号、排序或数据类型方面），则可使用格式化文件。 有关详细信息，请参阅 [用来导入或导出数据的格式化文件 (SQL Server)](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="additional-examples"></a>其他示例  
 以下主题包含有关使用 **bcp**的示例：  
  
-   [创建格式化文件 (SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [批量导入和导出 XML 文档的示例 (SQL Server)](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [批量导入数据时保留标识值 (SQL Server)](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [指定字段终止符和行终止符 (SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [准备用于批量导出或导入的数据 (SQL Server)](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [SET QUOTED_IDENTIFIER (Transact-SQL)](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sp_tableoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)   
 [用来导入或导出数据的格式化文件 (SQL Server)](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
