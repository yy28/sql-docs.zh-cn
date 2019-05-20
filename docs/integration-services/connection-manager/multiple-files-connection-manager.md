---
title: 多文件连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- Multiple Files connection manager
- connection managers [Integration Services], Multiple Files
- connections [Integration Services], files
- multiple file connections
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fb4be4efb5c9cce7273bb9024b7b2b3a5565af16
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728164"
---
# <a name="multiple-files-connection-manager"></a>多文件连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  多文件连接管理器使包可以在运行时引用现有的文件和文件夹，或者创建文件和文件夹。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的内置任务和数据流组件不使用多文件连接管理器。 但是，可以在脚本任务或脚本组件中使用此连接管理器。 有关如何在脚本任务中使用连接管理器的信息，请参阅 [Connecting to Data Sources in the Script Task](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)。 有关如何在脚本组件中使用连接管理器的信息，请参阅 [Connecting to Data Sources in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
## <a name="usage-types-of-the-multiple-files-connection-manager"></a>多文件连接管理器的使用类型  
 多文件连接管理器的 **FileUsageType** 属性指定如何使用连接。 多文件连接管理器可以创建文件、创建文件夹、使用现有文件以及使用现有文件夹。  
  
 下表列出了 **FileUsageType**的值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0**|多文件连接管理器使用现有文件。|  
|**1**|多文件连接管理器创建文件。|  
|**2**|多文件连接管理器使用现有文件夹。|  
|**3**|多文件连接管理器创建文件夹。|  
  
## <a name="configuration-of-the-multiple-files-connection-manager"></a>多文件连接管理器的配置  
 向包中添加多文件连接管理器时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时解析为多文件连接的连接管理器，设置多文件连接属性，并将多文件连接添加到包的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **MULTIFILE**。  
  
 可以按以下方法配置多文件连接管理器：  
  
-   指定文件和文件夹的使用类型。  
  
-   指定文件和文件夹。  
  
-   如果使用多个文件或文件夹，指定访问文件和文件夹的顺序。  
  
 如果多文件连接管理器引用了多个文件和文件夹，那么文件和文件夹的路径应由竖线 (|) 分开。 连接管理器的 **ConnectionString** 属性的格式如下：  
  
 \<路径>|\<路径>  
  
 也可以用通配符指定多个文件或文件夹。 例如，若要引用 C 驱动器上的所有文本文件，可以将 **ConnectionString** 属性的值设置为 C:\\*.txt。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [“添加文件连接管理器”对话框 UI 参考](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
  
