---
title: 启用包日志记录在 SQL Server 数据工具 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a93245b97bf7c6c382f533c6d6e317b399f9e54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172494"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中启用包日志记录
  本过程介绍如何将日志添加到包中，如何配置包级日志记录，以及如何将日志记录配置保存为 XML 文件。 您只能在包级添加日志，但包不必执行日志记录，就可以在包所包括的容器中启用日志记录。  
  
> [!IMPORTANT]  
>  如果您将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器，则为包执行设置的日志记录级别优先于使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]配置的包日志记录。  
  
 默认情况下，包中的容器与其父容器使用相同的日志记录配置。 有关为各个容器设置日志记录选项的信息，请参阅 [使用保存的配置文件配置日志记录](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md)。  
  
### <a name="to-enable-logging-in-a-package"></a>在包中启用日志记录  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在 **SSIS** 菜单上，单击 **“日志记录”**。  
  
3.  在 **“提供程序类型”** 列表中，选择一个日志提供程序，然后单击 **“添加”**。  
  
4.  在“配置”列中，选择连接管理器或单击“\<新建连接>”以为日志提供程序新建一个适当类型的连接管理器。 根据所选提供程序的不同，可以使用下列某个连接管理器：  
  
    -   对于文本文件，请使用文件连接管理器。 有关详细信息，请参阅 [File Connection Manager](connection-manager/file-connection-manager.md)  
  
    -   对于 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]，请使用文件连接管理器。  
  
    -   对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请使用 OLE DB 连接管理器。 有关详细信息，请参阅 [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md)。  
  
    -   对于 Windows 事件日志，无需执行任何操作。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 自动创建日志。  
  
    -   对于 XML 文件，请使用文件连接管理器。  
  
5.  对于要在包中使用的每个日志，请重复步骤 3 和步骤 4。  
  
    > [!NOTE]  
    >  一个包可以使用多个同一类型的日志。  
  
6.  还可以选中包级复选框，选择要用于包级日志记录的日志，然后单击“详细信息”选项卡。  
  
7.  在 **“详细信息”** 选项卡上，选择 **“事件”** 将记录所有日志项，清除 **“事件”** 可以选择单个事件。  
  
8.  还可以单击 **“高级”** 指定要记录的信息。  
  
    > [!NOTE]  
    >  默认情况下会记录所有信息。  
  
9. 在“详细信息”选项卡上，单击“保存”。 将显示 **“另存为”** 对话框。 找到要将日志记录配置保存到的文件夹，为新的日志配置键入文件名，然后单击 **“保存”**。  
  
10. 单击“确定” 。  
  
11. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;日志记录](performance/integration-services-ssis-logging.md)   
 [Integration Services (SSIS) 日志记录](performance/integration-services-ssis-logging.md)  
  
  
