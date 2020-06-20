---
title: 查看包对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8ab1a510ec348ca30ffd1b8946b71ab935c0057c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972517"
---
# <a name="view-package-objects"></a>查看包对象
  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中， **“包资源管理器”** 选项卡提供包的资源管理器视图。 该视图反映了 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 体系结构的容器层次结构。 包容器位于层次结构的顶层，您可以展开包来查看连接、可执行文件、事件处理程序、日志提供程序、优先约束和包中的变量。

 可执行文件（包中的容器和任务）可以包含事件处理程序、优先约束和变量。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支持嵌套的容器层次结构，而 For 循环容器、Foreach 循环容器以及序列容器可包含其他可执行文件。

 如果包包含数据流， **包资源管理器** 将列出数据流任务，并包含列有数据流组件的 **“组件”** 文件夹。

 可以从 **“包资源管理器”** 选项卡中删除包中的对象，并访问 **“属性”** 窗口来查看对象属性。

 下面的关系图显示一个简单包的树视图。

 ![“包资源管理器”选项卡的屏幕快照](media/packageexplorer.gif "“包资源管理器”选项卡的屏幕快照")

### <a name="to-view-package-content"></a>查看包内容

-   [在包资源管理器中查看包对象](../../2014/integration-services/view-package-objects-in-package-explorer.md)

## <a name="see-also"></a>另请参阅
 [Integration Services 任务](control-flow/integration-services-tasks.md) [Integration Services 容器](control-flow/integration-services-containers.md)[优先约束](control-flow/precedence-constraints.md) [INTEGRATION SERVICES &#40;Ssis&#41; 变量](integration-services-ssis-variables.md)Integration Services &#40;[Ssis&#41; 事件处理程序](integration-services-ssis-event-handlers.md)Integration Services [&#40;ssis&#41; 日志记录](performance/integration-services-ssis-logging.md)


