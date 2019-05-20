---
title: 静态数据掩码 | Microsoft Docs
ms.date: 04/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: aliceku
ms.author: aliceku
manager: ajayj
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1cf3b95ec5836ac86770bd0cd9784f0617b91846
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580972"
---
# <a name="static-data-masking"></a>静态数据掩码
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

静态数据掩码作为 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) 18.0 预览版 5 及更高版本的组件发布。 
> [!IMPORTANT]
> 我们已确定当前原型未达到客户期望。 因此，我们之后不会包含此功能。 如果有替换候选项，我们将在计划中通知你最新动态。
>



![静态数据掩码](../../relational-databases/security/media/sql-static-data-masking/static_data_masking_intro_image.PNG)


## <a name="what-is-static-data-masking"></a>静态数据掩码是什么？ 
静态数据掩码是 SQL Server Management Studio 的一项功能，用户可以通过它创建数据库的掩码副本。 该功能是为需要在团队之间或者与其他组织共享数据（有的数据为敏感数据）的组织而开发的。 

静态数据掩码使用新数据（掩码后的数据）替换敏感数据（掩码前的数据），有助于以下场景： 
- 开发和测试 
- 分析和业务报告 
- 故障排除 
- 与顾问、研究团队或任何第三方共享数据库 

下面的示例展示静态数据掩码的实际运作情况。 掩码前，该列包含社会安全号码。 掩码后，每个社会安全号码的前五位数字已替换为随机生成的数字。

| 美国社会安全号码（掩码前）   | 美国社会安全号码（掩码后）  |
| ------------- | ------------- |
| 140-38-9110 | 302-92-9110 |
| 463-34-5535 | 189-70-5535 |
| 116-30-8733 | 201-01-8733 |
| 209-36-1971 | 683-10-1971 |
| 372-38-6948 | 372-38-6948 |
| 267-64-2334 | 100-03-2334 |
| 523-93-4176 | 582-20-4176 |
| 573-91-5137 | 730-20-5137 |
| 612-72-1026 | 369-40-1026 |

静态数据掩码的用户可以在多个掩码函数中进行选择。 掩码前和掩码后的数据可能高度相关或完全不相关，具体取决于掩码函数。 执行随机替换操作的掩码函数使数据在掩码前后高度相关。 

| 美国社会安全号码（掩码前） | 美国社会安全号码（掩码后） |
| ------------- | ------------- |
| 140-38-9110 | 612-72-1026 |  
| 463-34-5535 | 372-38-6948 | 
| 116-30-8733 | 523-93-4176 |
| 209-36-1971 | 209-36-1971 | 
| 372-38-6948 | 140-38-9110 |
| 267-64-2334 | 463-34-5535 | 
| 523-93-4176 | 573-91-5137 | 
| 573-91-5137 | 267-64-2334 | 
| 612-72-1026 | 116-30-8733 |

执行替换为 NULL 值操作的掩码函数使数据在掩码前后并无关联。 
 
| 美国社会安全号码（掩码前） | 美国社会安全号码（掩码后） |
| ------------- | ------------- |
| 140-38-9110 | NULL |  
| 463-34-5535 | NULL | 
| 116-30-8733 | NULL |
| 209-36-1971 | NULL | 
| 372-38-6948 | NULL |
| 267-64-2334 | NULL | 
| 523-93-4176 | NULL | 
| 573-91-5137 | NULL | 
| 612-72-1026 | NULL |

## <a name="how-does-static-data-masking-work"></a>静态数据掩码的工作原理是什么？
静态数据掩码发生在列级别。 用户选择要进行掩码操作的列，并为所选的每一列选择要应用的掩码函数。 有数个掩码函数可供选择。 [掩码函数](#masking-functions)详细介绍了这几个函数。 

然后，静态数据掩码将创建数据库的副本。 对于 Azure SQL 数据库，通过[复制函数](https://azure.microsoft.com/blog/static-data-masking-preview/)来创建副本。 对于 SQL Server，则通过先执行备份操作再执行还原操作来创建副本。 自此，静态数据掩码开始根据所选掩码函数，为每一列将掩码的前数据替换为掩码的后数据。 

在存储级别执行替换操作。 因此，静态数据掩码完成后，无法从数据库的掩码副本中检索掩码前数据。

## <a name="how-to-guide"></a>操作指南

下面是运行静态数据掩码的分步指南。 
 
1. 启动 SQL Server Management Studio。 连接到数据库。 在左侧的“对象资源管理器”窗格中，展开数据库文件夹。 右键单击要进行掩码的数据库。 左键单击“任务”。 左键单击“对数据库执行掩码...(预览)”。
 
 ![任务菜单](../../relational-databases/security/media/sql-static-data-masking/task_data_masking.PNG)
 
2. 掩码配置窗口弹出。 它将显示数据库中的所有表格。 这些表格以架构形式呈现，按架构中的字母顺序排序。 
 
 ![用户界面](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown.PNG)
 
3. 单击表名旁的下拉列表图标，获取表中所有列的列表。 对于表中各列，指定了其数据类型以及其是否可为 NULL。 可为 NULL 的列可以接收 NULL 值作为输入。 
 
 ![表格的下拉列表](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown_column.png)
 
4. 选择要进行掩码操作的列和要应用的掩码函数。 可用的掩码类型有：Shuffle 掩码、分组 Shuffle 掩码、单值掩码、NULL 掩码和字符串复合掩码。 
 
 ![掩码函数下拉列表](../../relational-databases/security/media/sql-static-data-masking/masking_functions.PNG)
 
 注意：大部分掩码函数有其他配置参数。 静态数据掩码为 Shuffle 掩码提供一个默认参数。 对于分组 Shuffle 掩码、单值掩码和字符串复合掩码，用户必须提供配置参数。 若要更改或提供配置参数，请单击“配置...”选项，然后在弹出的对话框中为参数指定（备用）值。 [掩码函数](#masking-functions)详细介绍了每个掩码函数。
 
 ![掩码函数配置按钮](../../relational-databases/security/media/sql-static-data-masking/masking_functions_configure.png)
 
 对于与配置和架构相关的错误和警告，掩码配置选项即时获得验证。  检测到的任何内容都将在左侧显示为图标，可将鼠标悬停在图标上获取其他详细信息。 
 
 在下面的示例中，用户为不允许使用 NULL 值（非 NULL 约束）的列选择了 NULL 掩码。
 
 ![验证机制错误](../../relational-databases/security/media/sql-static-data-masking/validation_mechanism_error_message.PNG)
 
 在下面的示例中，用户为单列选择了分组 Shuffle 掩码。 分组 Shuffle 最少需要两列，所以发出警告。 
 
 ![验证机制警告](../../relational-databases/security/media/sql-static-data-masking/validation_warning.PNG)
 
5. 可将完整的掩码配置另存为 XML 文件，以供将来使用。  尽管 Azure SQL 数据库和本地数据库之间的掩码函数配置相同，但保存的其他属性（例如备份文件路径）仍有一些细微的差别。 要保存配置，请单击“保存配置”、提供文件名，然后单击保存。  之后，用户便可使用“加载配置”来加载现有配置文件。我们建议为列数很多的表格使用配置文件。 
 
 ![配置文件](../../relational-databases/security/media/sql-static-data-masking/load_save_config.PNG)
 
6. 静态数据掩码将在用户的“文档”文件夹中创建一个名为“静态数据掩码”的文件夹并放入日志文件。 日志文件对调试十分有用。 日志文件的名称显示在配置窗口的底部。 
  
 
7. （仅限 SQL Server）如果对本地数据库执行静态数据掩码，则静态数据掩码将执行备份/还原操作。 在“步骤 2：克隆 .BAK 文件位置”中，提供备份文件在服务器上的存储位置。 

## <a name="masking-functions"></a>掩码函数

### <a name="null-masking"></a>NULL 掩码

NULL 掩码用 NULL 替换列中所有值。 如果列不接受 NULL 值，静态数据掩码工具将返回一个错误。 

### <a name="single-value-masking"></a>单值掩码

单值掩码用一个固定值替换列中的所有值，该固定值由用户指定。 输入的内容的格式必须可转换为所选列的类型。 要指定该值，点击“配置…”，提供一个值，然后点击“确定”。 

![单值掩码参数](../../relational-databases/security/media/sql-static-data-masking/single_value_parameter.PNG)


### <a name="shuffle-masking"></a>Shuffle 掩码

将列中的所有值随机打乱到新行中。 不生成新数据。 Shuffle 掩码提供保留列中 NULL 项的选项。 要执行此操作，请单击“配置...”，然后选择“保持 NULL 位置”框。

![Shuffle 掩码参数](../../relational-databases/security/media/sql-static-data-masking/shuffle_parameter.PNG)

下面是 Shuffle 掩码的示例，先打乱了 NULL 值，再使 NULL 值保留在原位。


| 美国社会安全号码（掩码前） | 美国社会安全号码（掩码后，打乱了 NULL 项） | 美国社会安全号码（掩码后，未打乱 NULL 项） |
| ------------- | ------------- | ------------- |
| 116-30-8733 | 612-72-1026 | 463-34-5535 |
| 140-38-9110 | NULL | 573-91-5137  |
| 209-36-1971 | 523-93-4176 | 140-38-9110 |
| NULL | 209-36-1971 | NULL |
| 463-34-5535 | 140-38-9110 | 116-30-8733  |
| 523-93-4176 | 463-34-5535 | 612-72-1026  |
| NULL | 573-91-5137 | NULL |
| 573-91-5137 | NULL | 523-93-4176 |
| 612-72-1026  | 116-30-8733  | 209-36-1971 |  

### <a name="group-shuffle-masking"></a>分组 Shuffle 掩码
在置乱组中，分组 Shuffle 将几列绑定在一起。 将置乱组中的各列作为一体一起打乱。 用户必须使用“配置...”选项指定置乱组的名称。

![分组 Shuffle 掩码参数](../../relational-databases/security/media/sql-static-data-masking/group_shuffle_parameter.PNG)

分组 Shuffle 发生在同一个表中；如果多个表使用了同一个置乱组名，则两个分组 Shuffle 为独立的操作。 组要包含的各列的组名必须相同。 该名称区分大小写。 同一个表中可以有多个置乱组（不同名称）。 

### <a name="string-composite-masking"></a>字符串复合掩码

字符串复合掩码根据某种模式生成随机字符串。 它专为必须遵循预定义模式才能成为有效项的字符串而设计。 例如，美国社会安全号码的格式为 123-45-6789。 在用户必须输入模式的对话框中指定字符串复合掩码的语法。

![字符串复合掩码参数](../../relational-databases/security/media/sql-static-data-masking/string_composite.PNG)

字符串复合掩码提供三个示例模式，单击这三个模式可以对其进行测试。 如果单击“电话号码”，模式框中将自动填充随机生成美国电话号码所需的公式。

![字符串复合掩码参数示例](../../relational-databases/security/media/sql-static-data-masking/string_composite_phone_example.PNG)

字符串复合掩码还具有高级模式，使用高级模式可以用模式生成的字符串替换现有数据的某些部分。 正则表达式中的捕获组决定字符串被替换的部分。 例如，可以替换电子邮件的用户名部分而保留域，或者替换电话号码而保留区域代码。 有关正则表达式的详细信息，请点击[此处](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference)。

![高级字符串复合掩码参数示例](../../relational-databases/security/media/sql-static-data-masking/string_composite_advanced.PNG)

字符串复合掩码和其高级模式仅可用于含 char、varchar、text、nchar、nvarchar 和 ntext [数据类型](../../t-sql/data-types/data-types-transact-sql.md)的列。

## <a name="limitations"></a>限制 

静态数据掩码具有以下限制：

- 不支持带[时态表](../../relational-databases/tables/temporal-tables.md)的数据库。

- 不对[内存优化](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)表进行掩码操作。

- 不对[计算列](../../relational-databases/tables/specify-computed-columns-in-a-table.md)和[标识](../../t-sql/statements/create-table-transact-sql-identity-property.md)列进行掩码操作。

- 静态数据掩码不支持 Azure SQL 超大规模数据库。

- 也不支持几何和地理数据类型。 

此外，它的掩码能力有以下三个限制：

- 静态数据掩码不更新[直方图统计信息](../../relational-databases/statistics/statistics.md)。 于是，静态数据掩码操作完成后，数据库掩码副本的直方图统计信息中可能仍包含敏感数据。 请考虑运行[更新统计信息](../../t-sql/statements/update-statistics-transact-sql.md)以补救此问题。 

- 如果静态数据掩码返回错误，则暂停所有掩码操作。 数据库副本不会被删除，且可能包含敏感信息。 如果静态数据掩码返回错误，则用户负责删除数据库副本。 

- （仅限 SQL Server）静态数据掩码操作完成后，[数据文件](../../relational-databases/databases/database-files-and-filegroups.md)和[日志文件](../../relational-databases/logs/the-transaction-log-sql-server.md)可能仍然在未分配的内存中包含少量敏感数据。 如果有权访问数据文件和日志文件，使用十六进制编辑器可能可以检索这些敏感数据。

## <a name="see-also"></a>另请参阅  
 [动态数据掩码](../../relational-databases/security/dynamic-data-masking.md)   
 [SQL 数据库静态数据掩码入门](https://azure.microsoft.com/documentation/articles/sql-database-static-data-masking-get-started/)  
