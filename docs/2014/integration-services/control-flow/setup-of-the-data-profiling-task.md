---
title: 设置数据事件探查任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], configuring
ms.assetid: fe050ca4-fe45-43d7-afa9-99478041f9a8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 54422b13b39de1e39f86ad653ecea95cdca02784
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918270"
---
# <a name="setup-of-the-data-profiling-task"></a>设置数据事件探查任务
  在可以查看源数据的配置文件之前，第一步是设置和运行数据事件探查任务。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包内创建此任务。 若要配置数据事件探查任务，可以使用数据事件探查任务编辑器。 使用此编辑器，可以选择输出配置文件的位置以及要计算哪些配置文件。 设置此任务后，可以运行包来计算数据配置文件。  
  
## <a name="requirements-and-limitations"></a>要求和限制  
 数据事件探查任务仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的数据。 它不适用于第三方或基于文件的数据源。  
  
 而且，若要运行包含数据事件探查任务的包，必须使用对 tempdb 数据库具有读/写权限（包括 CREATE TABLE 权限）的帐户。  
  
## <a name="data-profiling-task-in-a-package"></a>包中的数据事件探查任务  
 数据事件探查任务只配置配置文件并创建包含所计算配置文件的输出文件。 若要查看此输出文件，必须使用数据配置文件查看器，它是一个独立的查看器程序。 因为必须独立查看输出，所以可以在不包含任何其他任务的包中使用数据事件探查任务。  
  
 但是，您不必将数据事件探查任务用作包中的唯一任务。 如果希望在更复杂的包中的工作流或数据流中执行数据事件探查，您有如下选择：  
  
-   若要在包的控制流中实现基于该任务的输出文件的条件逻辑，请将脚本任务放置在数据事件探查任务之后。 然后可以使用此脚本任务查询输出文件。  
  
-   若要在加载并转换了数据流中的数据之后对该数据进行事件探查，则必须将更改后的数据暂时保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 然后，您可以对保存的数据进行事件探查。  
  
 有关详细信息，请参阅 [合并包工作流中的数据分析任务](incorporate-a-data-profiling-task-in-package-workflow.md)。  
  
## <a name="setup-of-the-task-output"></a>设置任务输出  
 在将数据事件探查任务放置到包中之后，必须设置任务将计算的配置文件的输出。 若要设置配置文件的输出，可以使用数据事件探查任务编辑器的 **“常规”** 页。 除了指定输出的目标外， **“常规”** 页还提供了用于执行数据快速配置文件的功能。 选择 **“快速配置文件”** 时，数据事件探查任务使用某些或所有具有默认设置的默认配置文件对表或视图进行事件探查。  
  
 有关详细信息，请参阅[数据事件探查任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)和[单个表快速配置文件窗体（数据事件探查任务）](data-profiling-task.md)。  
  
> [!IMPORTANT]  
>  输出文件可能包含有关数据库的敏感数据和数据库所包含的数据。 有关如何使此文件更加安全的建议，请参阅 [对包使用的文件的访问](../access-to-files-used-by-packages.md)。  
  
## <a name="selection-and-configuration-of-the-profiles-to-be-computed"></a>选择和配置要计算的配置文件  
 设置输出文件后，必须选择要计算的数据配置文件。 数据事件探查任务可以计算 8 个不同的数据配置文件。 其中的 5 个配置文件分析单列，其余的 3 个则分析多列或列和表之间的关系。 在单个数据事件探查任务中，可以为多列或多个表或视图中的列组合计算多个配置文件。  
  
 下表介绍其中的每个配置文件所计算的报告，以及配置文件对其有效的数据类型。  
  
|计算对象|帮助标识|使用此配置文件|  
|----------------|-------------------------|----------------------|  
|所选列中字符串值的所有不同长度和每个长度表示的行在表中的百分比。|**无效的字符串值 -** 例如，如果对某列进行事件探查，假定该列使用两个字符来表示美国的州代码，但发现它的值长于两个字符。|**列长度分布-** 对具有下列其中一种数据类型的列有效：<br /><br /> 字符数据类型：`char`、`nchar`、`varchar` 和 `nvarchar`|  
|一组正则表达式，涵盖字符串列中指定的百分比值。<br /><br /> 还可以查找将来可用于验证新值的正则表达式|**无效或格式不正确的字符串值-** 例如，邮政编码列的模式配置文件可能会生成正则表达式： \d {5} -\d {4} 、\d {5} 和 \d {9} 。 如果输出中包含其他正则表达式，则数据包含的值可能无效或者格式不正确。|**列模式配置文件-** 对具有下列其中一种数据类型的列有效：<br /><br /> 字符数据类型：`char`、`nchar`、`varchar` 和 `nvarchar`|  
|所选列中 null 值的百分比。|**列中 null 值的比率意外升高**。例如，您对应该包含美国邮政编码的列进行事件探查，但发现缺少邮政编码的高百分比。|**列 Null 比率-** 对具有以下数据类型的列有效：<br /><br /> 任何数据类型。 包括 `image`、`text`、`xml`、用户定义类型和变量类型。|  
|数值列的最小值、最大值、平均值和标准偏差等统计信息，以及 `datetime` 列的最小值和最大值。|**无效的数值和日期**—例如，您对历史日期列进行分析，但发现未来的最大日期。|**列统计信息配置文件-** 对具有下列其中一种数据类型的列有效：<br /><br /> 数值数据类型：整数类型（`bit` 除外）、`money`、`smallmoney`、`decimal`、`float`、`real` 和 `numeric`<br /><br /> 日期和时间数据类型：`datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2` 和 `datetimeoffset`<br />请注意：对于具有日期和时间数据类型的列，配置文件仅计算最小值和最大值。|  
|所选列中的所有非重复值以及每个值表示的行在表中的百分比。 或者表示大于表中指定百分比的值。|**列中的非重复值的数目不正确**-例如，你分析了包含美国中的状态的列，但发现了50多个非重复值。|**列值分布-** 对具有下列其中一种数据类型的列有效：<br /><br /> 数值数据类型：整数类型（`bit` 除外）、`money`、`smallmoney`、`decimal`、`float`、`real` 和 `numeric`<br /><br /> 字符数据类型：`char`、`nchar`、`varchar` 和 `nvarchar`<br /><br /> 日期和时间数据类型：`datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2` 和 `datetimeoffset`|  
|一列或者一组列是所选表的键或者近似键。|**可能的键列中有重复的值-** 例如，在 Customers 表中分析名称和地址列，并发现名称和地址组合应是唯一的重复值。|**候选键-** 多列配置文件，用于报告一列或一组列是否适合用作所选表的键。 具有以下数据类型的列有效：<br /><br /> 整数数据类型：`bit`、`tinyint`、`smallint`、`int` 和 `bigint`<br /><br /> 字符数据类型：`char`、`nchar`、`varchar` 和 `nvarchar`<br /><br /> 日期和时间数据类型：`datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2` 和 `datetimeoffset`|  
|一个区，对于该区来说，一列（依赖列）中的值取决于其他列或另一组列（决定列）中的值。|**在依赖列中无效的值-** 例如，对包含美国邮政编码的列与美国中包含状态的列之间的依赖关系进行分析。 相同的邮政编码对应的州应该总是相同的。 但是，在配置文件中发现依赖关系冲突。|**函数依赖关系-** 对具有以下其中一种数据类型的列有效：<br /><br /> 整数数据类型：`bit`、`tinyint`、`smallint`、`int` 和 `bigint`<br /><br /> 字符数据类型：`char`、`nchar`、`varchar` 和 `nvarchar`<br /><br /> 日期和时间数据类型：`datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2` 和 `datetimeoffset`|  
|列或者一组列适合用作所选表间的外键。<br /><br /> 即，此配置文件报告两列或两组列之间的重叠值。|**无效的值-** 例如，对 Sales 表的 ProductID 列进行分析。 在配置文件中发现，该列所包含的某些值不能在 Products 表的 ProductID 列中找到。|**值包含-** 对具有以下其中一种数据类型的列有效：<br /><br /> 整数数据类型：`bit`、`tinyint`、`smallint`、`int` 和 `bigint`<br /><br /> 字符数据类型： `char` 、 `nchar` 、 `varchar` 和`nvarchar`<br /><br /> 日期和时间数据类型：`datetime`、`smalldatetime`、`timestamp`、`date`、`time`、`datetime2` 和 `datetimeoffset`|  
  
 若要选择要计算的配置文件，可使用数据事件探查任务编辑器的 **“配置文件请求”** 页。 有关详细信息，请参阅[数据分析任务编辑器（“配置文件请求”页）](data-profiling-task-editor-profile-requests-page.md)。  
  
 在 **“配置文件请求”** 页中，还可以指定数据源并配置数据配置文件。 配置任务时，请考虑以下信息：  
  
-   若要简化配置并更轻松地发现不熟悉的数据的特征，可以使用通配符 **（ \* ）** 代替单个列名。 如果使用此通配符，任务将对具有相应数据类型的每个列进行事件探查，这可能会降低处理速度。  
  
-   当所选表或视图为空时，数据事件探查任务不会计算任何配置文件。  
  
-   当所选列中的所有值为 null 值时，数据事件探查任务只计算列 Null 比率配置文件。 它不计算列长度分布配置文件、列模式配置文件、列统计信息配置文件或空列的列值分布配置文件。  
  
 每个可用的数据配置文件都有自己的配置选项。 有关这些选项的详细信息，请参阅下面的主题：  
  
-   [候选键配置文件请求选项（数据事件探查任务）](candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [列长度分布配置文件请求选项（数据事件探查任务）](column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [列 Null 比率配置文件请求选项（数据事件探查任务）](column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [列模式配置文件请求选项（数据事件探查任务）](column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [列统计信息配置文件请求选项（数据事件探查任务）](column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [列值分布配置文件请求选项（数据事件探查任务）](column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [函数依赖关系配置文件请求选项（数据事件探查任务）](functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [值包含配置文件请求选项（数据事件探查任务）](value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="execution-of-the-package-that-contains-the-data-profiling-task"></a>执行包含数据事件探查任务的包  
 设置数据事件探查任务后，可以运行此任务。 此任务随后将计算数据配置文件并以 XML 格式将此信息输出到一个文件或包变量中。 此 XML 结构符合 DataProfile.xsd 架构。 您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 或其他架构编辑器、XML 编辑器或记事本等文本编辑器中打开该架构。 此数据质量信息架构可用于以下目的：  
  
-   在单位内和跨单位交换数据质量信息。  
  
-   生成处理数据质量信息的自定义工具。  
  
 目标命名空间在架构中将标识为 [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/) 。  
  
## <a name="next-step"></a>后续步骤  
 [数据配置文件查看器](data-profile-viewer.md)。  
  
  
