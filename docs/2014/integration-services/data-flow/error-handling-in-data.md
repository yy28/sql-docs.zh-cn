---
title: 数据中的错误处理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ecae86e05bc67275d21d0811d3b1abd642a7e62c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201617"
---
# <a name="error-handling-in-data"></a>数据中的错误处理
  数据流组件将转换应用到列数据、从源提取数据或将数据加载到目标中时，可能会发生错误。 错误常因意外数据值而发生。 例如，如果列包含字符串而不是数字，数据转换将失败；在数据库列中执行插入操作时，如果数据是日期而列的数据类型为数值，此操作将失败；如果因列值为零而导致数学运算无效，表达式将无法计算。  
  
 错误通常属于下列类别之一：  
  
-   数据转换错误，其在转换导致重要数字丢失、非重要数字丢失和字符串截断时发生。 如果不支持请求的转换，也会发生数据转换错误。  
  
-   表达式计算错误，其在运行时计算的表达式执行无效运算，或因数据值丢失或错误而出现语法错误时发生。  
  
-   查找错误，其在查找操作在查找表中找不到匹配时发生。  
  
 许多数据流组件支持错误输出，这使得您可以控制组件处理传入和传出数据中行级错误的方式。 通过设置输入或输出中各个列的选项，可以指定发生截断或错误时组件的行为。 例如，可以指定组件应在客户名称数据被截断时失败，但忽略另一包含不太重要数据的列上的错误。  
  
 错误输出可以连接到另一个转换的输入，或者加载到非错误输出以外的目标。 例如，错误输出可以连接到为空白列提供字符串的派生列转换。  
  
 下列关系图显示包含错误输出的简单数据流。  
  
 ![具有错误输出的数据流](../media/mw-dts-11.gif "Data flow with error output")  
  
 除数据列外，错误输出还包含 **ErrorCode** 列和 **ErrorColumn** 列。 **ErrorCode** 列标识错误，而 **ErrorColumn** 列则包含错误列的沿袭标识符。 若要查看这些列的元数据，请单击将错误输出连接到数据流中下一个组件的路径。 在某些环境下， **ErrorColumn** 列的值会设置为零。 当错误条件影响到整行而不是单列时，就会发生该情况。 例如，在查找转换中的查找失败时。  
  
 有关详细信息，请参阅 [数据流](data-flow.md) 和 [Integration Services 路径](integration-services-paths.md)。  
  
 有关 Integration Services 的错误、警告和其他消息的列表，请参阅 [Integration Services Error and Message Reference](../integration-services-error-and-message-reference.md)。  
  
## <a name="error-and-truncation-options"></a>错误和截断选项  
 错误属于两个类别之一：错误或截断。 错误指示确定的失败，并且生成 NULL 结果。 此类错误可以包括数据转换错误或表达式计算错误。 例如，尝试将包含字母字符的字符串转换为数字将导致错误。 数据转换、表达式计算和对变量、属性和数据列的表达式结果分配可能会由于非法转换和不兼容的数据类型而失败。 有关详细信息，请参阅[转换 (SSIS 表达式)](../expressions/cast-ssis-expression.md)、[表达式中的 Integration Services 数据类型](../expressions/integration-services-data-types-in-expressions.md)和 [Integration Services 数据类型](integration-services-data-types.md)。  
  
 截断的严重程度小于错误。 截断生成的结果可能是有用的甚至是所希望的。 您可以将截断视为错误或可接受的情况。 例如，如果将 15 个字符的字符串插入只有一个字符宽度的列，您可以截断该字符串。  
  
 可以配置源、转换和目标处理错误和截断的方式。 下表对这些选项进行说明：  
  
|选项|Description|  
|------------|-----------------|  
|组件失败|发生错误或截断时数据流任务失败。 失败是错误或截断的默认选项。|  
|忽略失败|忽略错误或截断，并且将数据行定向到转换或源的输出。|  
|重定向行|将错误或截断的数据行定向到源、转换或目标的错误输出。|  
  
## <a name="adding-the-error-description"></a>添加错误说明  
 默认情况下，错误输出提供了数值错误代码，并且通常包含发生错误的列的标识符。 通过使用脚本的单独一行来调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 接口的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法，可以使用脚本组件来包括其他列中的错误说明。  
  
 可以将脚本组件添加到数据流的错误段中希望捕获其错误的数据流组件下游的任何位置，但通常在错误行被写入目标之前立即将其放入。 这样，脚本只查找已写入的错误行的说明。 例如，数据流的错误段可能纠正某些错误，并且不将这些行写入错误目标。 有关详细信息，请参阅[增强错误输出使用脚本组件](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)。  
  
### <a name="to-configure-an-error-output"></a>配置错误输出  
  
-   [在数据流组件中配置错误输出](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>请参阅  
 [数据流](data-flow.md)   
 [使用转换对数据进行转换](transformations/transform-data-with-transformations.md)   
 [使用路径连接组件](../connect-components-with-paths.md)   
 [数据流任务](../control-flow/data-flow-task.md)   
 [数据流](data-flow.md)  
  
  
