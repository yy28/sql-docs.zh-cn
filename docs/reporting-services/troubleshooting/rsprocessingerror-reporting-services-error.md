---
title: "rsProcessingError-Reporting Services 错误 |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
caps.latest.revision: 29
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7065e2f766ec3ce56bed2d9b3bc0e90c5290b6ea
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rsProcessingError|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|处理报表时出错。|  
  
## <a name="explanation"></a>解释  
 在发布、处理、本地预览、从报表服务器中查看或者为报表创建订阅时，遇到了一个或多个错误。 此错误消息表示至少检测到了一个错误。  
  
### <a name="possible-causes"></a>可能的原因  
 可能的原因包括：  
  
-   报表服务器上发生处理错误。  
  
-   预览报表时，在本地报表处理期间发生处理错误。  
  
-   组表达式的计算结果为错误的数据类型。  
  
-   筛选器定义指定了两个表达式，它们的计算结果为无法比较的数据类型。  
  
-   表达式引用的字段在字段集合中不存在。  
  
-   表达式包含的聚合函数调用具有无效或有冲突的作用域。  
  
-   表达式引用的参数在报表参数集合中不存在。  
  
-   无法加载未正确部署的自定义程序集或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 程序集。  
  
-   将 Nullable 属性设置为 **False** 的参数检测到该参数中包含 Null 值。  
  
-   数据区域的 Hidden 属性的表达式包含以下错误：对象引用未设置为某个对象的实例。  
  
-   表达式包含的函数调用无效或有语法错误。  
  
## <a name="user-action"></a>用户操作  
  
### <a name="finding-more-information"></a>查找详细信息  
 执行下列一种或多种操作：  
  
-   如果是从报表服务器查看报表或将报表视为订阅，请查看错误消息的全文。 扩充文本中提供了详细信息。  
  
-   如果在报表设计器中创作报表，并在预览或发布报表时出现该错误，则会在“错误列表”窗口中提供其他信息。  
  
-   如果在报表设计器预览中创作报表，请查看完整的错误消息文本。 扩充文本中提供了详细信息。  
  
-   如果是在报表服务器上查看报表，并且是以报表服务器上的本地管理员身份运行，则可以通过右键单击页并选择“查看源”来查看调用堆栈。 调用堆栈中提供了详细信息。  
  
-   如果以本地管理员身份在报表服务器上运行，请在日志文件中搜索 `ReportProcessingException`。 日志项包含详细信息。 报表服务器日志文件位于通常\<*驱动器*>: files\microsoft SQL Server\MSRS12。MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*datetimestamp*。 日志。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
### <a name="failed-to-load-expression-host-assembly"></a>无法加载表达式宿主程序集。  
 自定义程序集必须设置了强名称签名和 AllowPartiallyTrustedCallers 属性。 有关详细信息，请参阅 [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md) 和 [Understanding Security Policies](../../reporting-services/extensions/secure-development/understanding-security-policies.md)。  
  
### <a name="a-built-in-global-name-does-not-exist"></a>内置全局名称不存在  
 检查表达式的拼写。 内置全局名称、参数名称和字段名称均区分大小写。 在导致错误的表达式中，检查该名称在报表中是否实际存在以及拼写是否正确。 有关详细信息，请参阅[表达式中的内置集合（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)。  
  
### <a name="parameter-properties-and-null"></a>参数属性和 Null  
 多值参数不能为 Null。 有关详细信息，请参阅[报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>无法处理包含子报表的主报表  
 必须使用相同版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表处理器来处理包含子报表的报表。 将报表升级到报表定义架构的当前版本时，可能会同时更新主报表和子报表，也可能不会。 如果报表与其子报表的版本不兼容，则会显示以下消息：“无法处理子报表”。  
  
 必须更改主报表或子报表，以便使用相同版本的报表处理器来处理所有报表。 有关报表为何无法进行升级的信息，请参阅 [升级报表](../../reporting-services/install-windows/upgrade-reports.md)。  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>验证函数调用为 Visual Basic 而不是 SQL  
 可以在针对关系数据库的查询文本中使用 SQL 函数。 不能在查询文本中使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函数。  
  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，表达式可以使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函数、System.Math 或 System.String 函数、完全限定的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 函数或自定义函数（以自定义代码或自定义程序集形式提供）。 不能在表达式中使用 SQL 函数。  
  
 验证查询和表达式中进行的函数调用是否有效。  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>无法比较筛选器的数据类型  
 在筛选器公式中，定义筛选内容的筛选器表达式和筛选器值必须为相同数据类型才能进行比较。 如果出现以下错误之一，请修改字段表达式或筛选器值以使数据类型匹配：  
  
-   处理*\<报表项类型 >*为*\<报表项名称 >*无法执行。 无法比较类型的数据*\<类型 >*和*\<类型 >*。 请检查返回的数据类型*\<报表项名称 >*。  
  
-   无法评估*\<属性名称 >*。  
  
-   无法评估*\<属性名称 >*。 它所引用的数据集字段包含错误： *\<错误字符串 >*。  
  
 有关详细信息，请参阅[对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>聚合函数调用中指定的作用域无效或有冲突  
 如果 Tablix 单元中包含对表达式的聚合函数调用，报表处理器将使用单元所属的最内部组的作用域来计算表达式。  
  
 也可以将特定作用域的名称传递给聚合函数。 作用域可以引用数据集和数据区域的名称，也可以引用位于数据层次结构中较高位置的作用域的名称。 这适用于以下消息：  
  
-   *\<报表项类型 >* *\<报表项名称 >*具有无效的作用域"*\<作用域名称 >*"。 该作用域必须是当前作用域或包含在当前作用域内。  
  
-   *\<属性名称 >*表达式*\<报表项类型 >* *\<报表项名称 >*具有无效的聚合函数的作用域参数。 作用域参数必须设置为字符串常量，该常量可以等于所包含组的名称、所包含数据区域的名称或数据集的名称。  
  
 对于计算运行总计的聚合函数（**Previous**、 **RunningValue**或 **RowNumber**），可以将作用域参数指定为行组名称或列组名称，但不能同时指定二者。 这适用于以下错误消息：  
  
-   **以前**， **RunningValue**或**RowNumber**聚合函数中的数据单元格使用*\<报表项类型 >* *\<报表项名称 >*的分组的行和列中的作用域，请参阅*\<报表项类型 >*。 所有的作用域参数**上一步**， **RunningValue**和**RowNumber**聚合函数内的*\<报表项类型 >*可以引用行分组或数据列分组，但不是两个。  
  
 有关详细信息，请参阅[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)和[表达式中的内置集合（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)。  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>顶级文本框的默认数据集作用域  
 如果报表包含多个数据集，请勿使用添加到报表设计图面上的文本框的默认作用域。 应使用一个表达式，其中包含数据集名称（作为作用域）和聚合函数。 例如， `=First(Fields!FieldName.Value, "DataSet2")`。  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [聚合函数引用 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [常用筛选器 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [数据集字段集合 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [自定义代码和在报表设计器 &#40; 中的表达式的程序集引用SSRS &#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [参数的集合引用 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
