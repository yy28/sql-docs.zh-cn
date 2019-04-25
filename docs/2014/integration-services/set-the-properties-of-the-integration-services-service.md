---
title: 设置 Integration Services 服务的属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- Integration Services service, properties
ms.assetid: 3a8ad546-0f58-4b31-ab56-58d6313b1098
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b9382a04977fae7db3442cb58caba1850cbcc14f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766621"
---
# <a name="set-the-properties-of-the-integration-services-service"></a>设置 Integration Services 服务的属性
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理并监视 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的包。 首次安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]时， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务会启动，启动类型设置为自动。  
  
 安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务后，可以使用 SQL Server 配置管理器或 Services MMC 管理单元设置其属性。  
  
 若要配置该服务的其他重要功能（包括在何处存储和管理包），则必须修改服务的配置文件。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)。  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>使用 SQL Server 配置管理器设置 Integration Services 服务的属性  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”**、 **“Microsoft SQL Server”** 和 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
2.  在“SQL Server 配置管理器”管理单元中，在服务列表中找到 **SQL Server Integration Services**，右键单击 **SQL Server Integration Services**，然后单击“属性”。  
  
3.  在 **“SQL Server Integration Services 属性”** 对话框中，可以执行下列操作：  
  
    -   单击 **“登录”** 选项卡以查看诸如帐户名等登录信息。  
  
    -   单击 **“服务”** 选项卡以查看有关服务的信息（例如，主机计算机的名称），并指定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的启动模式。  
  
        > [!NOTE]  
        >  “高级”选项卡不包含 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的信息。  
  
4.  单击 **“确定”**。  
  
5.  在“文件”菜单上，单击“退出”以关闭“SQL Server 配置管理器”管理单元。  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>使用“服务”设置 Integration Services 服务的属性  
  
1.  在 **“控制面板”** 中，如果使用的是经典视图，请单击 **“管理工具”**；如果使用的是分类视图，请单击 **“性能和维护”** ，再单击 **“管理工具”**。  
  
2.  单击 **“服务”**。  
  
3.  在“服务”管理单元中，在服务列表中找到 **SQL Server Integration Services**，右键单击 **SQL Server Integration Services**，再单击“属性”。  
  
4.  在 **“SQL Server Integration Services 属性”** 对话框中，可以执行下列操作：  
  
    -   单击 **“常规”** 选项卡。若要启用该服务，请选择手动或自动启动类型。 若要禁用该服务，请选择 **“启动类型”** 框中的“禁用”。 选择“禁用”不会停止当前正在运行的服务。  
  
         如果该服务已经启用，则可以单击 **“停止”** 停止该服务，或单击 **“启动”** 启动该服务。  
  
    -   单击 **“登录”** 选项卡可查看或编辑登录信息。  
  
    -   单击 **“恢复”** 选项卡可查看服务失败时计算机的默认反应。 您可以修改这些选项以满足您环境的要求。  
  
    -   单击 **“依赖项”** 选项卡可查看依赖服务的列表。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务没有任何依赖项。  
  
5.  单击“确定” 。  
  
6.  另外，如果启动类型为“手动”或“自动”，还可以右键单击 **SQL Server Integration Services**，然后单击“启动”、“停止”或“重新启动”。  
  
7.  在“文件”菜单上，单击“退出”关闭“服务”管理单元。  
  
## <a name="see-also"></a>请参阅  
 [管理 Integration Services 服务](../../2014/integration-services/manage-the-integration-services-service.md)  
  
  
