---
title: 以编程方式运行和管理包 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6e2af58481babf1ba9e19465a67c530275db0402
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295688"
---
# <a name="running-and-managing-packages-programmatically"></a>以编程方式运行和管理包

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  如果您需要在开发环境之外管理和运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，可以采用编程方式对包进行操作。 如果采用这种方法，则您有多种选择：  
  
-   加载和运行现有包，不进行修改。  
  
-   加载现有包，对其进行重新配置（例如，针对一个不同的数据源），然后运行。  
  
-   创建一个新包，添加并配置组件（逐个对象和属性），保存并运行。  
  
 您可以只编写几行代码，从客户端应用程序加载和运行现有包。  
  
 本节介绍并演示如何以编程方式运行现有包，以及如何从其他应用程序访问数据流的输出。 作为高级编程选项，可以按照[以编程方式生成包](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)主题中的说明，已编程方式逐行创建 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
 本节还讨论其他可以用编程方式执行的管理任务，用于管理存储的包、正在运行的包和包角色。  
  
## <a name="running-packages-on-the-integration-services-server"></a>在 Integration Services 服务器上运行包  
 将包部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器时，可以使用 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间以编程方式运行包。 使用 .NET Framework 3.5 编译 Microsoft.SqlServer.Management.IntegrationServices 程序集。 如果您正在生成 .NET Framework 4.0 应用程序，可能需要将程序集引用直接添加到项目文件。  
  
 您还可以使用该命名空间在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上部署和管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。 有关命名空间和代码片段的概述，请参阅 blogs.msdn.com 上的博客文章 [SSIS 目录托管对象模型一瞥](https://go.microsoft.com/fwlink/?LinkId=253122)。  
  
## <a name="in-this-section"></a>本节内容  
 [了解本地执行与远程执行之间的差异](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 讨论在本地执行包和在服务器上执行包的重大差别。  
  
 [以编程方式加载和运行本地包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 介绍如何在本地计算机上从客户端应用程序执行现有包。  
  
 [以编程方式加载和运行远程包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 介绍如何从客户端应用程序执行现有包以及如何确保包在服务器上运行。  
  
 [加载本地包的输出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 介绍如何在本地计算机上执行包，以及如何使用 DataReader 目标和 DtsClient 命名空间将数据流输出加载到客户端应用程序。  
  
 [以编程方式枚举可用的包](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 介绍如何发现由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务管理的可用包。  
  
 [以编程方式管理包和文件夹](../../integration-services/run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 介绍如何创建、重命名和删除包与文件夹。  
  
 [以编程方式管理正在运行的包](../../integration-services/run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 介绍如何列出当前正在运行的包，如何检查其属性以及如何停止正在运行的包。  
  
 [以编程方式管理包角色（SSIS 服务）](../../integration-services/run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md)  
 介绍如何获取或设置有关分配给包或文件夹的角色的信息。  
  
## <a name="reference"></a>参考  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)  
 列出预定义的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码及其符号名称和说明。  
  
## <a name="related-sections"></a>相关章节  
 [用脚本扩展包](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 讨论如何使用脚本任务扩展控制流，以及如何使用脚本组件扩展数据流。  
  
 [用自定义对象扩展包](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 讨论如何创建用于多个包的编程自定义任务、数据流组件以及其他包对象。  
  
 [以编程方式生成包](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 讨论如何以编程方式创建、配置和保存 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
