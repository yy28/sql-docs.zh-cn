---
title: 开发自定义数据流组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a5a31cd9402fd448db6084b71b7c243de4b97f5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608165"
---
# <a name="developing-a-custom-data-flow-component"></a>开发自定义数据流组件
  数据流任务由一些组件组成，这些组件用于连接各种数据源，然后快速转换和路由数据。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供一个可扩展的对象模型，该模型允许开发人员创建可在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 和已部署的包中使用的自定义源、转换和目标。 本节包含的主题将指导您开发自定义数据流组件。  
  
## <a name="in-this-section"></a>本节内容  
 [创建自定义数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
 介绍创建自定义数据流组件的初始步骤。  
  
 [数据流组件的设计时方法](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
 介绍要在自定义数据流组件中实现的设计时方法。  
  
 [数据流组件的运行时方法](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
 介绍要在自定义数据流组件中实现的运行时方法。  
  
 [执行计划和缓冲区分配](../../../integration-services/extending-packages-custom-objects/data-flow/execution-plan-and-buffer-allocation.md)  
 介绍数据流执行计划和数据缓冲区的分配。  
  
 [在数据流中使用数据类型](../../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)  
 介绍数据流如何将 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型映射到 .NET Framework 托管数据类型。  
  
 [验证数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)  
 介绍用于验证组件配置和重新配置组件元数据的方法。  
  
 [实现外部元数据](../../../integration-services/extending-packages-custom-objects/data-flow/implementing-external-metadata.md)  
 介绍如何使用外部元数据列进行数据验证。  
  
 [在数据流组件中引发和定义事件](../../../integration-services/extending-packages-custom-objects/data-flow/raising-and-defining-events-in-a-data-flow-component.md)  
 介绍如何引发预定义事件和自定义事件。  
  
 [在数据流组件中记录和定义日志条目](../../../integration-services/extending-packages-custom-objects/data-flow/logging-and-defining-log-entries-in-a-data-flow-component.md)  
 介绍如何创建和写入自定义日志条目。  
  
 [在数据流组件中使用错误输出](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
 介绍如何将错误行重定向到备用输出。  
  
 [升级数据流组件的版本](../../../integration-services/extending-packages-custom-objects/data-flow/upgrading-the-version-of-a-data-flow-component.md)  
 介绍如何在首次使用新版本的组件时更新已保存的组件元数据。  
  
 [为数据流组件开发用户界面](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
 介绍如何实现组件的自定义编辑器。  
  
 [开发特定类型的数据流组件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 包含开发三种类型的数据流组件（源、转换和目标）的相关信息。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 包含用于创建自定义数据流组件的类和接口。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 包含组成数据流任务对象模型并且可用于创建自定义数据流组件或生成数据流任务的类和接口。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 包含用于创建数据流组件的用户界面的类和接口。  
  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)  
 列出预定义的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 错误代码及其符号名称和说明。  
  
## <a name="related-sections"></a>相关章节  
  
### <a name="information-common-to-all-custom-objects"></a>所有自定义对象的通用信息  
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的所有类型自定义对象的通用信息，请参阅以下主题：  
  
 [开发 Integration Services 的自定义对象](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 介绍实现 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的所有自定义对象类型的基本步骤。  
  
 [使自定义对象持久化](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 介绍自定义持久性并在必要时作出解释。  
  
 [生成、部署和调试自定义对象](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 介绍生成、签名、部署和调试自定义对象的技术。  
  
### <a name="information-about-other-custom-objects"></a>其他自定义对象的信息  
 有关可在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的其他自定义对象类型的信息，请参阅以下主题：  
  
 [开发自定义任务](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 讨论如何对自定义任务进行编程。  
  
 [开发自定义连接管理器](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 讨论如何对自定义连接管理器进行编程。  
  
 [开发自定义日志提供程序](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 讨论如何对自定义日志提供程序进行编程。  
  
 [开发自定义 ForEach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 讨论如何对自定义枚举器进行编程。  
  
## <a name="see-also"></a>另请参阅  
 [使用脚本组件扩展数据流](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [比较脚本解决方案和自定义对象](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
