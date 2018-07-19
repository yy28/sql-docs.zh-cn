---
title: Azure Data Lake Analytics 任务 | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 395d790069294aed541f9756fa7caefbb62f9a7b
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854409"
---
# <a name="azure-data-lake-analytics-task"></a>Azure Data Lake Analytics 任务

Azure Data Lake Analytics 任务允许用户将 U-SQL 作业提交到 Azure Data Lake Analytics 服务。 [Azure Data Lake Analytics (ADLA)](https://azure.microsoft.com/services/data-lake-analytics/)。

“Azure Data Lake Analytics 任务”是[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组件。

## <a name="configure-the-azure-data-lake-analytics-task"></a>配置 Azure Data Lake Analytics 任务

若要将 Azure Data Lake Analytics 任务添加到某个包，请将它从 SSIS 工具箱拖到设计器区域中。 然后双击该任务，或右键单击该任务并选择“编辑”，以打开“Azure Data Lake Analytics 任务编辑器”对话框。 可以通过 SSIS 设计器或以编程方式来设置属性。

## <a name="general-page-configuration"></a>常规页配置

使用“常规”页配置 Azure Data Lake Analytics 任务，并提供任务提交的 U-SQL 脚本。 若要了解有关 U-SQL 语言的详细信息，请参阅 [U-SQL 语言参考](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/u-sql-language-reference)。

### <a name="basic-configuration"></a>基本配置

- 名称：指定 Azure Data Lake Analytics 任务的名称。
- 说明：指定 Azure Data Lake Analytics 任务的说明。

### <a name="u-sql-configuration"></a>U-SQL 配置

U-SQL 配置具有两个设置：“SourceType”和基于“SourceType”值的动态选项。 

- SourceType：指定 U-SQL 脚本的源。 在 SSIS 程序包执行期间，脚本将被提交到 Azure Data Lake Analytics 帐户。 此属性具有下表所列的 3 个选项。

|ReplTest1|描述|  
|-----------|-----------------|  
|DirectInput|通过内联编辑器指定 U-SQL 脚本。 选择此值将显示动态选项 USQLStatement。|  
|**文件连接**|指定包含 U-SQL 脚本的本地 .usql 文件。 选择此选项将显示动态选项 FileConnection。|  
|**变量**|指定包含 U-SQL 脚本的 SSIS 变量。 选择此值将显示动态选项 **SourceVariable**。|

- SourceType 动态选项：指定 U-SQL 查询的脚本内容。 

|SourceType|动态选项|  
|-----------|-----------------|  
|SourceType = DirectInput|直接在选项框中键入要提交的 U-SQL 查询，或单击浏览按钮 (...) 在“输入 U-SQL 查询”对话框中键入 U-SQL 查询。|  
|SourceType = FileConnection|选择现有文件连接管理器，或单击“<新建连接...>”，创建新的文件连接。 相关文章：[文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
|SourceType = 变量|选择现有变量，或单击“\<新建变量...>”，创建一个新变量。 相关文章：[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)|


### <a name="job-configuration"></a>作业配置
作业配置指定 U-SQL 作业提交属性。

- AzureDataLakeAnalyticsConnection：指定提交 U-SQL 脚本的 Azure Data Lake Analytics 帐户。 从已定义的连接管理器的列表中选择连接。 要创建新连接，请选择“<新建连接>”。 相关文章：[Azure Data Lake Analytics 连接管理器](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)。

- JobName：指定 U-SQL 作业的名称。 
- AnalyticsUnits：指定 U-SQL 作业的分析单位计数。
- 优先级：指定 U-SQL 作业的优先级。 可将优先级设置为 0 到 1000 之间的数字，数字越低，优先级越高。
- RuntimeVersion：指定 U-SQL 作业的 Azure Data Lake Analytics 运行时版本。 默认情况下，此选项设置为“默认”。 通常无需更改此属性。
- Synchronous：指定任务是否等待作业执行完成的布尔值。 设置为 True 时，任务将被标记为在作业完成后成功。 设置为 False 时，任务将被标记为在作业进入准备阶段后成功。

|ReplTest1|描述|
|-----------|-----------------|
|True|任务结果基于 U-SQL 作业执行结果。 作业成功 --> 任务成功；作业失败 --> 任务失败；作业成功或失败 --> 任务完成。|
|False|任务结果基于 U-SQL 作业提交和准备结果。 作业提交成功并进入准备阶段 --> 任务成功；作业提交失败或作业在准备阶段失败 --> 任务失败；任务成功或失败 --> 任务完成。|

- TimeOut：指定作业执行的超时时间（以秒为单位）。 在作业超时后，该作业将被取消，且任务将被标记为失败。如果“同步”被设置为“False”，则 TimeOut 属性将不可用。 如果“同步” 被设置为“false”，则 TimeOut 属性将不可用。

## <a name="parameter-mapping-page-configuration"></a>参数映射页配置

使用“Azure Data Lake Analytics 任务编辑器”对话框的“参数映射”页将变量映射到 U-SQL 脚本中的参数（U-SQL 变量）。

- 变量名称：通过单击“添加”添加了参数映射之后，请从列表中选择系统变量或用户定义的变量，或单击\<“新建变量...>”以使用“添加变量”对话框添加新变量。 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)  

- 参数名称：提供 U-SQL 脚本中的参数/变量名称。 请确保参数名称以 @ 符号开头，例如 @Param1。 

以下是如何将参数传递到 U-SQL 脚本的示例。

示例 U-SQL 脚本
```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

在上面的脚本示例中，在 **@in** 和 **@out** 参数中定义了输入和输出路径。 U-SQL 脚本中的 **@in** 和 **@out** 参数的值通过“参数映射”配置动态传递。

|“变量名称”|参数名称|
|-------------|--------------|
|用户：Variable1|@in|
|用户：Variable2|@out| 

## <a name="expression-page-configuration"></a>表达式页配置

常规页配置中的所有属性都可以被分配为属性表达式，以在运行时启用属性的动态更新。 相关主题：[在包中使用属性表达式](../../integration-services/expressions/use-property-expressions-in-packages.md)

## <a name="see-also"></a>另请参阅
- [Azure Data Lake Analytics Connection Manager](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Azure Data Lake Store 文件系统任务](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Azure Data Lake Store 连接管理器](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

