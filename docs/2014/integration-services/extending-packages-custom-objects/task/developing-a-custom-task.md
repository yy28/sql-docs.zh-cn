---
title: 开发自定义任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f597ee3a063da534267f7d4674a024a8fcc02f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62896138"
---
# <a name="developing-a-custom-task"></a>开发自定义任务
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]使用任务执行工作单元，从而支持数据的提取、转换和加载。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含多种任务，这些任务可执行从执行 SQL 语句到从 FTP 站点下载文件的大部分常用操作。 如果包含的任务和支持的操作不能完全满足您的要求，您可以创建自定义任务。  
  
 若要创建自定义任务，必须创建从 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 基类继承的类，再将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性应用到新类，然后重写基类的重要方法和属性，包括 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法。  
  
## <a name="in-this-section"></a>本节内容  
 本节介绍如何创建、配置和编写自定义任务及其可选自定义用户界面的代码。  
  
 [创建自定义任务](creating-a-custom-task.md)  
 介绍第一个步骤，即创建自定义任务。  
  
 [编写自定义任务代码](coding-a-custom-task.md)  
 介绍如何编写自定义任务的主要方法的代码。  
  
 [在自定义任务中连接数据源](connecting-to-data-sources-in-a-custom-task.md)  
 介绍如何将自定义任务连接到数据源。  
  
 [在自定义任务中引发和定义事件](raising-and-defining-events-in-a-custom-task.md)  
 介绍如何从自定义任务引发事件和定义自定义事件。  
  
 [在自定义任务中添加对调试的支持](adding-support-for-debugging-in-a-custom-task.md)  
 介绍如何在自定义任务中创建断点目标。  
  
 [为自定义任务开发用户界面](developing-a-user-interface-for-a-custom-task.md)  
 介绍如何创建显示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中用于配置自定义任务属性的用户界面。  
  
## <a name="related-sections"></a>相关章节  
  
### <a name="information-common-to-all-custom-objects"></a>所有自定义对象的通用信息  
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的所有类型自定义对象的通用信息，请参阅以下主题：  
  
 [开发 Integration Services 的自定义对象](../developing-custom-objects-for-integration-services.md)  
 介绍实现 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的所有类型自定义对象的基本步骤。  
  
 [使自定义对象持久化](../persisting-custom-objects.md)  
 介绍自定义持久性并在必要时作出解释。  
  
 [生成、部署和调试自定义对象](../building-deploying-and-debugging-custom-objects.md)  
 介绍生成、签名、部署和调试自定义对象的技术。  
  
### <a name="information-about-other-custom-objects"></a>其他自定义对象的信息  
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的其他类型自定义对象的信息，请参阅以下主题：  
  
 [开发自定义连接管理器](../connection-manager/developing-a-custom-connection-manager.md)  
 讨论如何对自定义连接管理器进行编程。  
  
 [开发自定义日志提供程序](../log-provider/developing-a-custom-log-provider.md)  
 讨论如何对自定义日志提供程序进行编程。  
  
 [开发自定义 ForEach 枚举器](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 讨论如何对自定义枚举器进行编程。  
  
 [开发自定义数据流组件](../data-flow/developing-a-custom-data-flow-component.md)  
 讨论如何对自定义数据流源、转换和目标进行编程。  
  
![Integration Services 图标（小）](../../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [使用脚本任务扩展包](../../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [比较脚本解决方案和自定义对象](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
