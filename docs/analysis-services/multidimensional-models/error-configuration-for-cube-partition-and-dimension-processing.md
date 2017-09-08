---
title: "多维数据集、 分区和维度处理的错误配置 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.cubeproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.partitionproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.dimensionproperties.errorconfiguration.f1
ms.assetid: 3f442645-790d-4dc8-b60a-709c98022aae
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 83259b46fd10b45e25e032dfdb692fd654c67260
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="error-configuration-for-cube-partition-and-dimension-processing"></a>多维数据集、 分区和维度处理的错误配置
  有关多维数据集、分区或维度对象的错误配置属性决定了当处理过程中出现数据完整性错误时服务器的响应方式。 键列中的重复键、缺失键和空值通常会触发这类错误，尽管导致错误的记录不会添加到数据库中，不过您仍可以设置确定后续操作的属性。 默认情况下处理会停止。 但在多维数据集开发过程中，您可能希望在出现错误时继续进行处理，以便使用导入的数据测试多维数据集的行为（即使数据不完整）。  
  
 本主题包含以下各节：  
  
-   [执行顺序](#bkmk_exec)  
  
-   [默认行为](#bkmk_default)  
  
-   [错误配置属性](#bkmk_props)  
  
-   [在何处设置错误配置属性](#bkmk_tools)  
  
-   [缺失键 (KeyNotFound)](#bkmk_missing)  
  
-   [事实数据表中的 Null 外键 (KeyNotFound)](#bkmk_nullfact)  
  
-   [维度中的 Null 键](#bkmk_nulldim)  
  
-   [导致不一致关系的重复键 (KeyDuplicate)](#bkmk_dupe)  
  
-   [更改错误限制或错误限制操作](#bkmk_limit)  
  
-   [设置错误日志路径](#bkmk_log)  
  
-   [下一步](#bkmk_next)  
  
##  <a name="bkmk_exec"></a> 执行顺序  
 对于每个记录，服务器始终先执行 **NullProcessing** 规则，然后执行 **ErrorConfiguration** 规则。 了解这一点十分重要，因为当两个或更多错误记录在键列中具有零值时，将 Null 值转换为零值的 Null 值处理属性可能会在随后引入重复键错误。  
  
##  <a name="bkmk_default"></a> 默认行为  
 默认情况下，处理会在涉及键列的第一个错误出现时停止。 此行为由错误限制和停止处理指令控制，其中错误限制将允许错误数指定为零，而停止处理指令告知服务器在达到错误限制时停止处理。  
  
 由于 null 值、缺失值或重复值而触发错误的记录会转换为未知成员或被弃用。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不会导入违反数据完整性约束的数据。  
  
-   由于 **ConvertToUnknown** 的 **KeyErrorAction**设置，默认操作是转换为未知成员。 分配给未知成员的记录会在数据库中进行隔离，作为您在处理完成之后可能要调查的问题证据。  
  
     未知成员会从查询工作负荷中排除，但是这些成员在某些客户端应用程序中可见（如果 **“UnknownMember”** 设置为 **“Visible”**）。  
  
     若要跟踪转换为未知成员的 null 值数目，可以修改 **NullKeyConvertedToUnknown** 属性以便向日志或在“处理”窗口中报告这些错误。  
  
-   手动将 **KeyErrorAction** 属性设置为 **DiscardRecord**时，会执行弃用操作。  
  
 通过错误配置属性，可以确定在出现错误时服务器的响应方式。 选项包括立即停止处理、继续处理但停止日志记录或继续处理并记录错误。 默认设置因错误严重性而异。  
  
 错误计数可跟踪出现的错误数。 设置上限时，服务器响应会在达到该限制时更改。 默认情况下，服务器在达到限制之后停止处理。 默认限制是 0，从而导致处理在出现进行计数的第一个错误时停止。  
  
 高影响错误（如键字段中缺失键或存在 null 值）应尽快解决。 默认情况下，这些错误遵循 **ReportAndContinue** 服务器行为，即服务器捕获错误，将其添加到错误计数，然后继续处理（错误限制为零时除外，这种情况下处理会立即停止）。  
  
 其他错误会生成，但是默认情况下不进行计数或记录（这是 **IgnoreError** 设置），因为错误不一定造成数据完整性问题。  
  
 错误计数受 null 值处理设置影响。 对于维度属性，null 值处理选项确定遇到 null 值时服务器的响应方式。 默认情况下，数字列中的 null 值会转换为零，而字符串列中的 null 值会作为空白字符串进行处理。 可以覆盖 **NullProcessing** 属性以便在 null 值导致 **KeyNotFound** 或 **KeyDuplicate** 错误之前捕获 null 值。 有关详细信息，请参阅 [维度中的 Null 键](#bkmk_nulldim) 。  
  
 错误会在“处理”对话框中进行记录，但不会保存。 可以指定键错误日志文件名以在文本文件中收集错误。  
  
##  <a name="bkmk_props"></a> 错误配置属性  
 有九个错误配置属性。 五个属性用于确定出现特定错误时的服务器响应。 其他四个属性的作用域是错误配置工作负荷，如允许的错误数、达到该限制时要执行的操作、是否在日志文件中收集错误。  
  
 **针对特定错误的服务器响应**  
  
|属性|默认|其他值|  
|--------------|-------------|------------------|  
|**CalculationError**<br /><br /> 当初始化错误配置时发生。|**IgnoreError** 不对错误进行记录和计数；只要错误计数低于最大限制，处理便会继续。|**ReportAndContinue** 对错误进行记录和计数。<br /><br /> **ReportAndStop** 报告错误并立即停止处理（与错误限制无关）。|  
|**KeyNotFound**<br /><br /> 当事实数据表中的外键在相关维度表中没有匹配主键时（例如，“销售量”事实数据表的某个记录的产品 ID 在“产品”维度表中不存在）发生。 此错误可能会在分区处理或雪花状维度的维度处理过程中发生。|**ReportAndContinue** 对错误进行记录和计数。|**ReportAndStop** 报告错误并立即停止处理（与错误限制无关）。<br /><br /> **IgnoreError** 不对错误进行记录和计数；只要错误计数低于最大限制，处理便会继续。 触发此错误的记录在默认情况下会转换为未知成员，但是您通过更改 **KeyErrorAction** 属性弃用这些记录。|  
|**KeyDuplicate**<br /><br /> 当在维度中发现重复属性键时发生。 在大多数情况下，存在重复属性键是可接受的，但是此错误会向您告知存在重复项，以便您可以检查维度中是否存在可能导致属性之间关系不一致的设计缺陷。|**IgnoreError** 不对错误进行记录和计数；只要错误计数低于最大限制，处理便会继续。|**ReportAndContinue** 对错误进行记录和计数。<br /><br /> **ReportAndStop** 报告错误并立即停止处理（与错误限制无关）。|  
|**NullKeyNotAllowed**<br /><br /> 当对维度属性设置 **NullProcessing** = **Error** 时，或当用于唯一标识成员的属性键列中存在 null 值时发生。|**ReportAndContinue** 对错误进行记录和计数。|**ReportAndStop** 报告错误并立即停止处理（与错误限制无关）。<br /><br /> **IgnoreError** 不对错误进行记录和计数；只要错误计数低于最大限制，处理便会继续。 触发此错误的记录在默认情况下会转换为未知成员，但您可以通过设置 **KeyErrorAction** 属性弃用这些记录。|  
|**NullKeyConvertedToUnknown**<br /><br /> 当 null 值随后转换为未知成员时发生。 对维度属性设置 **NullProcessing** = **ConvertToUnknown** 会触发此错误。|**IgnoreError** 不对错误进行记录和计数；只要错误计数低于最大限制，处理便会继续。|如果您将此错误视为参考信息，请保留默认值。 否则，可以选择 **ReportAndContinue** 以向“处理”窗口报告错误并针对错误限制对错误计数。<br /><br /> **ReportAndStop** 报告错误并立即停止处理（与错误限制无关）。|  
  
 **常规属性**  
  
|**属性**|**值**|  
|------------------|----------------|  
|**KeyErrorAction**|这是发生 **KeyNotFound** 错误时服务器执行的操作。 针对此错误的有效响应包括 **ConvertToUnknown** 或 **DiscardRecord**。|  
|**KeyErrorLogFile**|这是用户定义的文件名，必须具有 .log 文件扩展名，位于服务帐户拥有读/写权限的文件夹中。 此日志文件仅包含处理期间生成的错误。 如果您需要详细信息，请使用网络流量记录器。|  
|**KeyErrorLimit**|这是在处理失败前服务器将允许的最大数据完整性错误数目。 值为 -1 表示没有限制。 默认值为 0，表示处理在发生第一个错误时停止。 您还可以将其设置为整数。|  
|**KeyErrorLimitAction**|这是键错误数达到上限时服务器执行的操作。 设置为 **“停止处理”**时，处理立即终止。 设置为 **“停止日志记录”**时，处理继续进行，但是错误不再进行报告或计数。|  
  
##  <a name="bkmk_tools"></a> 在何处设置错误配置属性  
 使用部署数据库之后的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的属性页，或是 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的模型项目中的属性页。 两个工具中有相同的属性。 还可以在 msmdrsrv.ini 文件中设置错误配置属性以更改针对错误配置的服务器默认值，以及在 **Batch** 和 **Process** 命令（如果处理作为脚本操作运行）中设置这些属性。  
  
 可以对可作为独立操作处理的任何对象设置错误配置。  
  
#### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
  
1.  在“对象资源管理器”中，右键单击以下对象之一的“属性”：维度、多维数据集或分区。  
  
2.  在“属性”中，单击 **“错误配置”**。  
  
#### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
  
1.  在解决方案资源管理器中，双击某个维度或多维数据集。 **“ErrorConfiguration”** 随即出现在下方窗格的“属性”中。  
  
2.  或者，仅对于单个维度，在“解决方案资源管理器”中右键单击该维度，选择“处理”，然后在“处理维度”对话框中选择“更改设置”。 错误配置选项随即出现在“维度键错误”选项卡上。  
  
##  <a name="bkmk_missing"></a> 缺失键 (KeyNotFound)  
 缺失键值的记录无法添加到数据库中，即使在忽略错误或错误限制是无限时也是如此。  
  
 当事实数据表中的记录包含外键值，但是该外键在相关维度表中没有对应记录时，服务器会在分区处理过程中生成 **KeyNotFound** 错误。 当处理的相关或雪花状维度表中一个维度中的记录指定的外键在相关维度中不存在时，也会发生此错误。  
  
 发生 **KeyNotFound** 错误时，会将有问题的记录分配给未知成员。 此行为通过 **“键操作”**（设置为 **“ConvertToUnknown”**）进行控制，以便您可以查看分配的记录做进一步调查。  
  
##  <a name="bkmk_nullfact"></a> 事实数据表中的 Null 外键 (KeyNotFound)  
 默认情况下，事实数据表的外键列中的 Null 值转换为零。 假设零不是有效的外键值， **KeyNotFound** 错误会进行记录并针对错误限制（默认情况下是零）进行计数。  
  
 要允许处理继续进行，可以在转换 Null 值并检查是否存在错误之前处理 Null 值。 为此，请将 **“NullProcessing”** 设置为 **“Error”**。  
  
#### <a name="set-nullprocessing-property-on-a-measure"></a>对度量值设置 NullProcessing 属性  
  
1.  在 SQL Server Data Tools 的解决方案资源管理器中，双击多维数据集以便在多维数据集设计器中打开它。  
  
2.  在“度量值”窗格中右键单击某个度量值，然后选择“属性”。  
  
3.  在“属性”中，展开 **“源”** 以查看 **“NullProcessing”** 属性。 它在默认情况下设置为 **“Automatic”** ，这对于 OLAP 项，会将包含数字数据的字段的 null 值转换为零。  
  
4.  将该值更改为 **Error** 以排除任何具有 null 值的记录，从而避免进行 null 值到数字（零）转换。 通过此修改可以避免与键列中具有零值的多个记录相关的重复键错误，也可在零值外键在相关维度表中没有主键等效项时避免 **KeyNotFound** 错误。  
  
##  <a name="bkmk_nulldim"></a> 维度中的 Null 键  
 要在雪花状维度的外键中发现 null 值时继续处理，请通过对维度属性的 **NullProcessing** 设置 **KeyColumn** 先处理 null 值。 这会在 **KeyNotFound** 错误发生之前弃用或转换记录。  
  
 有两个选项用于对维度属性处理 null 值：  
  
-   设置 **NullProcessing**=**UnknownMember** 可将具有 null 值的记录分配给未知成员。 这会生成默认情况下忽略的 **NullKeyConvertedToUnknown** 错误。  
  
-   设置 **NullProcessing**=**Error** 可排除具有 null 值的记录。 这会生成要进行记录并针对键错误限制进行计数的 **NullKeyNotAllowed** 错误。 可以在 **“不允许 Null 键”** 上将错误配置属性设置为 **IgnoreError** ，以允许处理继续进行。  
  
 Null 值对于非键字段可能是个问题，因为 MDX 查询根据 Null 值是解释为零值还是空值返回不同结果。 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供 Null 值处理选项，使您可以预定义所需的转换行为。 有关详细信息，请参阅 [定义未知成员和 Null 处理属性](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) 和 <xref:Microsoft.AnalysisServices.NullProcessing> 。  
  
#### <a name="set-nullprocessing-property-on-a-dimension-attribute"></a>对维度属性设置 NullProcessing 属性  
  
1.  在 SQL Server Data Tools 的解决方案资源管理器中，双击维度以便在维度设计器中打开它。  
  
2.  在“属性”窗格中右键单击某个属性，然后选择“属性”。  
  
3.  在“属性”中，展开 **“KeyColumns”** 以查看 **“NullProcessing”** 属性。 它在默认情况下设置为 **“Automatic”** ，这会将包含数字数据的字段的 null 值转换为零。 请将该值更改为 **“Error”** 或 **“UnknownMember”**。  
  
     此修改通过在检查记录是否存在错误之前弃用或转换记录，消除触发 **“KeyNotFound”** 的底层条件。  
  
     根据错误配置，这些操作中的任意一个都可以导致进行报告和计数的错误。 可能需要调整其他属性（如将 **KeyNotFound** 设置为 **ReportAndContinue** 或将 **KeyErrorLimit** 设置为非零值），以便在对这些操作进行报告和计数时允许处理继续进行。  
  
##  <a name="bkmk_dupe"></a> 导致不一致关系的重复键 (KeyDuplicate)  
 默认情况下，存在重复键不会停止处理，但是会忽略该错误，并从数据库中排除重复记录。  
  
 要更改此行为，请将 **KeyDuplicate** 设置为 **ReportAndContinue** 或 **ReportAndStop** 以报告错误。 随后可以检查错误以确定维度设计中的潜在缺陷。  
  
##  <a name="bkmk_limit"></a> 更改错误限制或错误限制操作  
 可以提高错误限制以允许处理过程中出现更多错误。 没有有关提高错误限制的指南；合适的值因具体情况而异。 错误限制在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中通过 **ErrorConfiguration** 属性中的 **KeyErrorLimit** 进行指定，或是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中通过维度、多维数据集或度量值组属性的“错误配置”选项卡上的“错误数”进行指定。  
  
 达到错误限制之后，便可以指定处理停止或日志记录停止。 例如，假定对错误限制 100 将操作设置为 **StopLogging** 。 出现第 101 个错误时，处理继续进行，但是错误不再进行记录或计数。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，将错误限制操作指定为 **ErrorConfiguration** 属性中的 **KeyErrorLimitAction**，或是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，将其指定为维度、多维数据集或度量值组属性的“错误配置”选项卡上的“出错时要执行的操作”。  
  
##  <a name="bkmk_log"></a> 设置错误日志路径  
 可以指定文件以存储在处理过程中报告的键相关错误消息。 默认情况下，错误在交互处理过程中在“处理”窗口中可见，随后会在关闭窗口或会话时被弃用。 日志仅包含与键相关的错误信息，与处理对话框中报告的错误相同。  
  
 错误会记录到文本文件中，必须具有 .log 文件扩展名。 除非出现错误，否则该文件为空。 默认情况下，该文件会在 DATA 文件夹中创建。 可以指定另一个文件夹，只要 Analysis Services 服务帐户可以写入该位置即可。  
  
##  <a name="bkmk_next"></a> 下一步  
 决定错误是停止处理还是被忽略。 请记住，忽略的只是错误。 不会忽略导致错误的记录；该记录会被弃用或转换为未知成员。 违反数据完整性规则的记录绝不会添加到数据库中。 默认情况下，处理在出现第一个错误时停止，但是您可以通过提高错误限制来更改此行为。 在多维数据集开发中，放宽错误配置规则可能十分有用，从而允许处理继续进行，以便可以使用数据进行测试。  
  
 决定是否更改默认 null 值处理行为。 默认情况下，字符串列中的 null 值会作为空字符串进行处理，而数字列中的 null 值会作为零值进行处理。 有关对属性设置 null 值处理的说明，请参阅 [Defining the Unknown Member and Null Processing Properties](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) 。  
  
## <a name="see-also"></a>另请参阅  
 [日志属性](../../analysis-services/server-properties/log-properties.md)   
 [定义未知的成员和 Null 处理属性](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
  
