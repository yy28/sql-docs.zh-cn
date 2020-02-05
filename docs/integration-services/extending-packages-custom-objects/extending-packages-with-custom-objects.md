---
title: 用自定义对象扩展包 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 07454f4b273e6a0fab698574bb5d66cdd8adc7af
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71287235"
---
# <a name="extending-packages-with-custom-objects"></a>用自定义对象扩展包

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  如果觉得 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 内提供的组件不能满足您的需求，可以通过编写自己的扩展插件代码来扩展 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能。 对于扩展包，您有两种不同的选择：可以在脚本任务和脚本组件提供的功能强大的包装中编写代码，或者通过从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型提供的基类进行派生，完全重新创建自定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 扩展插件。  
  
 本节介绍这两种方法中较为高级的方法：使用自定义对象扩展包。  
  
 如果自定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 解决方案所需的灵活性要比脚本任务和脚本组件所具有的灵活性高，或如果需要可以在多个包中重复使用的组件，您可以通过 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型从头开始生成自定义任务、数据流组件和其他使用托管代码生成的包对象。  
  
## <a name="in-this-section"></a>本节内容  
 [开发 Integration Services 的自定义对象](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 讨论可以为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 创建的自定义对象，并概括介绍基本步骤和设置。  
  
 [使自定义对象持久化](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 讨论自定义对象的默认持久性和实现自定义持久性的过程。  
  
 [生成、部署和调试自定义对象](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 讨论生成、部署和测试各种类型自定义对象的常用方法。  
  
 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 介绍编写自定义任务代码的过程。  
  
 [开发自定义连接管理器](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 介绍编写自定义连接管理器代码的过程。  
  
 [开发自定义日志提供程序](../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 介绍编写自定义日志提供程序代码的过程。  
  
 [开发自定义 ForEach 枚举器](../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 介绍编写自定义枚举器代码的过程。  
  
 [开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 讨论如何对自定义数据流源、转换和目标进行编程。  
  
## <a name="reference"></a>参考  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)  
 列出预定义的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码及其符号名称和说明。  
  
## <a name="related-sections"></a>相关章节  
 [用脚本扩展包](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 讨论如何使用脚本任务扩展控制流，或使用脚本组件扩展数据流。  
  
 [以编程方式生成包](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 介绍如何以编程方式创建、配置、运行、加载、保存和管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
## <a name="see-also"></a>另请参阅  
 [比较脚本解决方案与自定义对象](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
