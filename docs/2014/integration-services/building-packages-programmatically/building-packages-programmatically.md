---
title: 以编程方式生成包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3d69416b36969e564b611d1b1274367b6ce5cb86
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84924968"
---
# <a name="building-packages-programmatically"></a>以编程方式生成包
  如果您需要动态创建包，或需要在开发环境之外管理和执行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，则可以采用编程方式对包进行操作。 如果采用这种方法，则有一系列选择：

-   加载并执行现有包，不进行修改。

-   加载现有包，对其进行重新配置（例如，指定一个不同的数据源），然后执行。

-   创建一个新包，添加并配置组件（逐个对象和属性），保存并执行。

 您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型，以任何托管编程语言编写可创建、配置和执行包的代码。 例如，您可能希望创建元数据驱动的包，它们可以基于所选数据源及其表和列，配置它们的连接或数据源、转换和目标。

 本节逐行介绍并演示如何以编程方式创建和配置包。 如果选择复杂性最低的包编程方式，只需加载并运行现有包，不需要进行[以编程方式运行和管理包](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)中所介绍的修改。

 这里没有介绍一种中间方式，即将一个现有包加载为模板，对其进行重新配置（例如，指定一个不同的数据源），然后执行。 您也可以使用本节中的信息，修改包中的现有对象。

> [!NOTE]
>  将现有包用作模板并修改数据流中的现有列时，您可能必须删除现有列并调用受影响组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法。

## <a name="in-this-section"></a>本节内容
 [以编程方式创建包](../building-packages-programmatically/creating-a-package-programmatically.md)描述如何以编程方式创建包。

 [以编程方式添加任务](../building-packages-programmatically/adding-tasks-programmatically.md)描述如何向包中添加任务。

 [以编程方式连接任务](../building-packages-programmatically/connecting-tasks-programmatically.md)介绍如何根据上一个任务或容器的执行结果来控制包中的容器和任务的执行。

 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)描述如何将连接管理器添加到包。

 [以编程方式使用变量](../building-packages-programmatically/working-with-variables-programmatically.md)描述如何在包执行期间添加和使用变量。

 [以编程方式处理事件](../building-packages-programmatically/handling-events-programmatically.md)描述如何处理包和任务事件。

 [以编程方式启用日志记录](../building-packages-programmatically/enabling-logging-programmatically.md)描述如何为包或任务启用日志记录，以及如何将自定义筛选器应用于记录事件。

 [以编程方式添加数据流任务](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)介绍如何添加和配置数据流任务及其组件。

 [以编程方式查找数据流组件](../building-packages-programmatically/discovering-data-flow-components-programmatically.md)描述如何检测本地计算机上安装的组件。

 [以编程方式添加数据流组件](../building-packages-programmatically/adding-data-flow-components-programmatically.md)描述如何将组件添加到数据流任务。

 [以编程方式连接数据流组件](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)介绍如何连接两个数据流组件。

 [以编程方式选择输入列](../building-packages-programmatically/selecting-input-columns-programmatically.md)描述如何从数据流中的上游组件向组件提供的输入列。

 [以编程方式保存包](../building-packages-programmatically/saving-a-package-programmatically.md)描述如何以编程方式保存包。

## <a name="reference"></a>引用
 [Integration Services 错误和消息引用](../integration-services-error-and-message-reference.md)列出预定义的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码及其符号名称和说明。

## <a name="related-sections"></a>相关章节
 [用脚本扩展包](../extending-packages-scripting/extending-packages-with-scripting.md)讨论如何使用脚本任务扩展控制流，以及如何使用脚本组件扩展数据流。

 [用自定义对象扩展包](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)讨论如何创建程序自定义任务、数据流组件和其他包对象以便在多个包中使用。

 [以编程方式运行和管理包](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)讨论如何枚举、运行和管理包以及存储包的文件夹。

## <a name="external-resources"></a>外部资源

-    [www.codeplex.com/MSFTISProdSamples](www.codeplex.com/MSFTISProdSamples) 上的 CodePlex 示例 [Integration Services 产品示例](https://go.microsoft.com/fwlink/?LinkID=131204)

-   blogs.msdn.com 上的博客文章[自定义扩展插件性能探查](https://go.microsoft.com/fwlink/?LinkId=238831)

![Integration Services 图标（小）](../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [SQL Server Integration Services](../sql-server-integration-services.md)


