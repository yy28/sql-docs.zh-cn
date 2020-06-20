---
title: 数据挖掘查询任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytask.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 93021fb7000bd7adccd467e04fb7cf3430db5efe
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84919438"
---
# <a name="data-mining-query-task"></a>数据挖掘查询任务
  数据挖掘查询任务根据 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]内置的数据挖掘模型运行预测查询。 预测查询通过使用挖掘模型来创建对新数据的预测。 例如，预测查询可以预测夏季可能销售多少帆板，或生成可能购买帆板的预期客户列表。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供执行其他商业智能操作的任务，如运行数据定义语言 (DDL) 语句和处理分析对象。  
  
 有关其他商业智能任务的详细信息，请单击下列主题之一：  
  
-   [Analysis Services 执行 DDL 任务](analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 处理任务](analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>预测查询  
 查询是数据挖掘扩展 (DMX) 语句。 DMX 语言是 SQL 语言的扩展，为对挖掘模型的操作提供支持。 有关如何使用 DMX 语言的详细信息，请参阅[数据挖掘扩展插件 (DMX) 引用](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
 该任务可以查询根据同一挖掘结构生成的多个挖掘模型。 挖掘模型是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的某种数据挖掘算法生成的。 数据挖掘查询任务引用的挖掘结构可能包含使用不同算法生成的多个挖掘模型。 有关详细信息，请参阅[挖掘结构（Analysis Services - 数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)和[数据挖掘算法（Analysis Services - 数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)。  
  
 数据挖掘查询任务运行的预测查询可返回单行或数据集结果。 返回单行的查询称为单独查询。例如，预测夏季可能销售多少帆船的查询将返回一个数字。 有关返回单行的预测查询的详细信息，请参阅[数据挖掘查询接口](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)。  
  
 查询结果将保存到表中。 如果数据挖掘查询任务指定名称的表已经存在，则任务可以在相同名称后追加数字来创建新表，也可以覆盖表内容。  
  
 如果结果包含嵌套，则在保存前将结果简化。 通过简化结果可将嵌套结果集更改为表。 例如，简化包含 **Customer** 列和 **Product** 嵌套列的嵌套结果时，将在 **Customer** 列中添加行，从而生成包含每个客户的产品数据的表。 例如，购买三个不同产品的客户将形成一个三行的表，每行都重复出现此客户，并在每行中包含不同的产品。 如果省略了 FLATTENED 关键字，则表将只包含 **Customer** 列，而且每个客户只占一行。 有关详细信息，请参阅 [SELECT (DMX)](/sql/dmx/select-dmx)。  
  
## <a name="configuration-of-the-data-mining-query-task"></a>配置数据挖掘查询任务  
 数据挖掘查询任务需要两个连接。 第一个连接是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器，连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例或包含挖掘结构和挖掘模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 第二个连接是 OLE DB 连接管理器，连接到包含任务要向其写入的表的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。 有关详细信息，请参阅 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md) 和 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [数据挖掘查询任务编辑器（“挖掘模型”选项卡）](../data-mining-query-task-editor-mining-model-tab.md)  
  
-   [数据挖掘查询任务编辑器（“查询”选项卡）](../data-mining-query-task-editor-query-tab.md)  
  
-   [数据挖掘查询任务编辑器（“输出”选项卡）](../data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  数据挖掘查询编辑器没有“表达式”页。 它使用 **“属性”** 窗口来访问工具，以便创建和管理数据挖掘查询任务的属性的属性表达式。  
  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>以编程方式配置数据挖掘查询任务  
 有关以编程方式设置这些属性的详细信息，请单击下列主题之一：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  
