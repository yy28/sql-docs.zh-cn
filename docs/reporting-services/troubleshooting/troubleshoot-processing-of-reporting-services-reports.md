---
title: Reporting Services 报表处理疑难解答 | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 85486e929683abaf99216a4d4b03c19a146f230c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573855"
---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>排除 Reporting Services 报表处理故障
检索报表数据后，报表处理器会将这些数据与布局信息组合。 将在组合的数据和布局的上下文中计算具有表达式的每个报表项属性。 使用本主题可以帮助解决这些问题。   
  
## <a name="my-report-definition-is-not-valid"></a>报表定义无效。  
在运行时，报表处理器会将数据和布局元素组合到报表定义中，并计算报表项属性的表达式。   
  
报表处理器会检查报表定义 (.rdl file) 是否符合 .rdl 文件开头的命名空间声明中指定的架构。 有关 RDL 架构的详细信息，请参阅 [查找报表定义架构版本 (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)。  
  
此外，在运行时计算的报表表达式必须符合一组规则，才能确保正确组合报表数据和布局。 报表处理器检测到问题时，您可能会看到以下消息：报表 `<report name>` 的定义无效。  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>报表项表达式只能引用当前数据集作用域中的字段；如果在聚合中，则只能引用指定数据集作用域中的字段。  
  
使用下面的列表可帮助确定错误原因：  
* 当报表具有多个数据集时，表体上文本框中的聚合表达式必须指定作用域参数。 例如， `=First(Fields!FieldName.Value, "DataSet1")`。  
  
若要指定作用域参数，请提供报表项所在作用域中的数据集、数据区域或组的名称。 有关详细信息，请参阅 [了解总计、聚合和内置集合的表达式作用域（Report Builder 3.0 和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 以及 [表达式引用（Report Builder 3.0 和 SSRS）](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md)。  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>对象名称的字符数必须大于 0 且小于等于 256。  
报表定义中对象标识符的长度最多为 256 个字符。 标识符必须区分大小写并符合 CLS。 名称必须以字母开头并且包含字母、数字或下划线 (_) 且不包含空格。 例如，文本框名称或数据区域名称必须符合这些规则。   
  
若要更改对象名称，请在“属性”窗格的工具栏中，在下拉列表中选择项，滚动到 **“名称”** ，然后输入有效对象名称。   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>文本框显示“#Error”，如何修复？  
当报表处理器在运行时计算报表项属性中的表达式，并检测到数据类型转换错误、作用域错误或其他错误时，会发出“#Error”消息。   
  
数据类型错误通常表示不支持默认数据类型或指定数据类型。 作用域错误表示计算表达式时指定作用域不可用。   
  
若要避免 #Error 消息，必须重写导致该错误的表达式。 若要确定有关该问题的更多详细信息，请查看详细错误消息。   
  
在预览模式下，在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)]查看输出窗口。 在报表服务器上查看调用堆栈。 
  
  
## <a name="see-also"></a>另请参阅  
[错误和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

