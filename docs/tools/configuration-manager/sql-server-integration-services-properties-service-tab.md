---
title: "SQL Server Integration Services 属性 （服务选项卡） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 37f0acd9-c96f-48fd-9b53-2ca0097af242
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 53b926557561d244dbef987aaabe3fdcfeabbf70
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-integration-services-properties-service-tab"></a>SQL Server Integration Services 属性（“服务”选项卡）
  使用“ **属性”对话框中的“服务”选项卡可以查看或指定下列选项** [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  。  
  
## <a name="options"></a>选项  
 **二进制路径**  
 显示此服务所使用的程序文件的位置。  
  
 **错误控制**  
 1 指示 `SERVICE_ERROR_NORMAL`。 如果在计算机启动过程中无法启动该服务，则启动程序会记录该错误并显示一个弹出消息框，但仍会继续执行启动操作。 此值不能更改。  
  
 **退出代码**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 错误代码，定义了在启动或停止服务时遇到的任何问题。 如果错误是此类表示的服务所特有的，并且 **ServiceSpecificExitCode** 属性中包含该错误的相关信息，则此属性将设置为 **ERROR_SERVICE_SPECIFIC_ERROR** (1066)。 当服务运行时，会将此值设置为 NO_ERROR (0)；而当服务正常终止时，会再次对它进行设置。  
  
 **Host Name**  
 显示运行 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务的计算机或群集的名称。  
  
 **名称**  
 指示该服务的显示名称。  
  
 **进程 ID**  
 显示 Windows 进程 ID。  
  
 **SQL 服务类型**  
 显示用于调用进程的服务的类型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装有多种服务。  
  
 **启动模式**  
 对此服务设置以下选项：  
  
-   手动：计算机启动时，此服务不自动启动。 您必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器或其他工具来启动该服务。  
  
-   自动：计算机启动时，此服务将尝试启动。  
  
-   已禁用：此服务无法启动。  
  
 **State**  
 指示此服务是正在运行、已停止还是已禁用。 **“...”**指示状态更改被挂起。  
  
  

