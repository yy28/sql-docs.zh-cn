---
title: "开发自定义 ForEach 枚举器 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 193fc8958826ac2bc382d5717a4f72690607a217
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-custom-foreach-enumerator"></a>开发自定义 ForEach 枚举器
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 使用 Foreach 枚举器可循环访问集合中的项并为每个元素执行相同的任务。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括支持常用集合的各种 Foreach 枚举器，例如文件夹中的所有文件、数据库中的所有表或包变量中存储的所有列表元素。 如果提供的 Foreach 枚举器和集合不能完全满足您的需要，您可以创建自定义 Foreach 枚举器。  
  
 若要创建 Foreach 枚举器，必须创建从 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 基类继承的类，再将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 属性应用到新类，然后重写基类的重要方法和属性，包括 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。  
  
## <a name="in-this-section"></a>本節內容  
 本节介绍如何创建、配置和编写自定义 Foreach 枚举器及其自定义用户界面的代码。  
  
 [创建自定义 Foreach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)  
 介绍如何为自定义 Foreach 枚举器项目创建类。  
  
 [编码的自定义 Foreach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
 介绍如何通过重写基类的方法和属性实现自定义 Foreach 枚举器。  
  
 [开发的自定义 ForEach 枚举器的用户界面](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 介绍如何实现用户界面类，以及用于配置自定义 Foreach 枚举器的窗体。  
  
## <a name="related-topics"></a>相关主题  
  
### <a name="information-common-to-all-custom-objects"></a>所有自定义对象的通用信息  
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的所有类型自定义对象的通用信息，请参阅以下主题：  
  
 [开发 Integration Services 的自定义对象](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 描述中实现的自定义对象的所有类型的基本步骤[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]。  
  
 [使自定义对象持久化](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 介绍自定义持久性并在必要时作出解释。  
  
 [生成、部署和调试自定义对象](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 介绍生成、签名、部署和调试自定义对象的技术。  
  
### <a name="information-about-other-custom-objects"></a>其他自定义对象的信息  
 有关可以在中创建的自定义对象的其他类型的信息[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]，请参阅以下主题：  
  
 [开发自定义任务](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 讨论如何对自定义任务进行编程。  
  
 [开发自定义连接管理器](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 讨论如何对自定义连接管理器进行编程。  
  
 [开发自定义日志提供程序](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 讨论如何对自定义日志提供程序进行编程。  
  
 [开发自定义数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 讨论如何对自定义数据流源、转换和目标进行编程。  
 

