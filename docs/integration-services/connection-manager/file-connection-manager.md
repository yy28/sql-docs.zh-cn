---
title: "文件连接管理器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f45869a6a4df80f2051ff52dd5566e6ca2576f3b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="file-connection-manager"></a>文件连接管理器
  文件连接管理器使包可以在运行时引用现有的文件或文件夹，或者创建文件或文件夹。 例如，您可以引用 Excel 文件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的某些组件使用文件中的信息来执行其工作。 例如，执行 SQL 任务可以引用包含该任务执行的 SQL 语句的文件。 其他组件对文件执行操作。 例如，文件系统任务可以引用一个文件，以便将其复制到新的位置。  
  
## <a name="usage-types-of-the-file-connection-manager"></a>文件连接管理器的使用类型  
 文件连接管理器的 **FileUsageType** 属性指定如何使用文件连接。 文件连接管理器可以创建文件、创建文件夹、使用现有文件或使用现有文件夹。  
  
 下表列出了 **FileUsageType**的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|文件连接管理器使用现有文件。|  
|**1**|文件连接管理器创建文件。|  
|**2**|文件连接管理器使用现有文件夹。|  
|**3**|文件连接管理器创建文件夹。|  
  
## <a name="multiple-file-or-folder-connections"></a>多个文件或文件夹连接  
 文件连接管理器只能引用一个文件或文件夹。 若要引用多个文件或文件夹，请使用多文件连接管理器，而不是文件连接管理器。 有关详细信息，请参阅 [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md)。  
  
## <a name="configuration-of-the-file-connection-manager"></a>文件连接管理器的配置  
 将文件连接管理器添加到包时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时解析为文件连接的连接管理器，设置该文件连接的属性，并将该文件连接添加到包的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **FILE**。  
  
 可以用下列方式配置文件连接管理器：  
  
-   指定使用类型。  
  
-   指定文件或文件夹。  
  
 通过在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的“属性”窗口中指定表达式，可以设置文件连接管理器的 ConnectionString 属性。 但为了避免在使用表达式指定文件或文件夹时出现验证错误，请在“文件连接管理器编辑器”中，为“文件/文件夹”添加文件或文件夹路径。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [文件连接管理器编辑器](../../integration-services/connection-manager/file-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="file-connection-manager-editor"></a>文件连接管理器编辑器
  可以使用 **“文件连接管理器编辑器”** 对话框指定用于连接文件或文件夹的属性。  
  
> [!NOTE]  
>  通过在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的“属性”窗口中指定表达式，可以设置文件连接管理器的 ConnectionString 属性。 但为了避免在使用表达式指定文件或文件夹时出现验证错误，请在“文件连接管理器编辑器”中，为“文件/文件夹”添加文件或文件夹路径。  
  
 若要了解有关文件连接管理器的详细信息，请参阅 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
### <a name="options"></a>“常规”  
 **使用类型**  
 指定“文件连接管理器”是连接到现有文件或文件夹，还是创建新的文件或文件夹。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|创建文件|在运行时创建新文件。|  
|现有文件|使用现有文件。|  
|创建文件夹|在运行时创建新文件夹。|  
|现有文件夹|使用现有文件夹。|  
  
 **文件/文件夹**  
 对于“文件”，请指定要使用的文件。  
  
 对于 **“文件夹”**，请指定要使用的文件夹。  
  
 **“浏览”**  
 通过使用“选择文件”或“查找文件夹”对话框选择文件或文件夹。  
  
  
