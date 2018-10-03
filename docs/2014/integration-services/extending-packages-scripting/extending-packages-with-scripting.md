---
title: 使用脚本扩展包 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b060579cfb55a1698007630240f86bdf4c170c5f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229267"
---
# <a name="extending-packages-with-scripting"></a>用脚本扩展包
  如果您觉得 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的内置组件不能满足您的要求，您可以编写自己的扩展插件代码来扩展 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能。 对于扩展包，您有两种不同的选择：可以在脚本任务和脚本组件提供的功能强大的包装中编写代码，或者通过从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型提供的基类进行派生，完全重新创建自定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 扩展插件。  
  
 本节介绍这两种方法中较为简单的方法：用脚本扩展包。  
  
 使用脚本任务和脚本组件，可以通过很少的编码对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的控制流和数据流进行扩展。 这两种对象均使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 开发环境和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 编程语言，并且均可使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类库和自定义程序集所提供的所有功能。 开发人员使用脚本任务和脚本组件创建自定义功能时，不必编写通常在开发自定义任务或自定义数据流组件时所需的所有基础结构代码。  
  
## <a name="in-this-section"></a>本节内容  
 [比较脚本任务和脚本组件](../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 讨论脚本任务与脚本组件之间的相似性和区别。  
  
 [比较脚本解决方案和自定义对象](comparing-scripting-solutions-and-custom-objects.md)  
 讨论在脚本解决方案与开发自定义对象之间进行选择的准则。  
  
 [引用脚本解决方案中的其他程序集](referencing-other-assemblies-in-scripting-solutions.md)  
 讨论在脚本项目中引用和使用外部程序集和命名空间所需的步骤。  
  
 [使用脚本任务扩展包](../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 讨论如何使用脚本任务来创建自定义任务。 通常，每次包执行会调用任务一次，包每次打开一个数据源也会调用任务一次。  
  
 [使用脚本组件扩展数据流](data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 讨论如何使用脚本组件来创建自定义数据流源、转换和目标。 通常，处理每一行数据时会调用一次数据流组件。  
  
## <a name="reference"></a>参考  
 [Integration Services 错误和消息引用](../integration-services-error-and-message-reference.md)  
 列出预定义的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码及其符号名称和说明。  
  
## <a name="related-sections"></a>相关章节  
 [用自定义对象扩展包](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 讨论如何创建用于多个包的编程自定义任务、数据流组件以及其他包对象。  
  
 [以编程方式生成包](../building-packages-programmatically/building-packages-programmatically.md)  
 介绍如何以编程方式创建、配置、运行、加载、保存和管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services** <br /> 有关最新的下载、 文章、 示例和视频[!INCLUDE[msCoName](../../includes/msconame-md.md)]，以及从社区获得所选的解决方案访问[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]MSDN 上的页面：<br /><br /> [访问 MSDN 上的 Integration Services 页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
