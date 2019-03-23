---
title: 为访问 SSIS 服务配置 Windows 防火墙 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3aab23efecc139e4aaf4a4c3d6d0075cf02a7e7f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387455"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>为访问 SSIS 服务配置 Windows 防火墙
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 Windows 防火墙系统可帮助防止通过网络连接对计算机资源进行未经授权的访问。 若要通过此防火墙访问 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，您必须将该防火墙配置为允许访问。  
  
> [!IMPORTANT]  
>  若要管理存储在某远程服务器上的包，您不必连接到该远程服务器上 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的实例。 只需编辑 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的配置文件，以便 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 显示存储在远程服务器上的包。 有关详细信息，请参阅 [配置 Integration Services 服务（SSIS 服务）](configuring-the-integration-services-service-ssis-service.md)的早期版本向后兼容。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务使用 DCOM 协议。 有关 DCOM 协议如何在防火墙下运作的详细信息，请参阅 MSDN Library 上的文章“[Using Distributed COM with Firewalls](https://go.microsoft.com/fwlink/?LinkId=12490)（与防火墙一起使用分布式 COM）”。  
  
 有很多可用的防火墙系统。 如果您运行的防火墙不是 Windows 防火墙，请查阅您的防火墙文档来获取特定于您所使用的系统的信息。  
  
 如果防火墙支持应用程序级筛选，则可以使用 Windows 提供的用户界面来指定允许通过该防火墙的例外项，如程序和服务。 否则，必须将 DCOM 配置为使用一组有限的 TCP 端口。 上面提供的 Microsoft 网站链接包含有关如何指定要使用的 TCP 端口的信息。  
  
 Integration Services 服务使用端口 135，该端口不能更改。 只有打开 TCP 端口 135 才能访问服务控制管理器 (SCM)。 SCM 执行以下任务：启动和停止 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，以及将控制请求传输到运行的服务。  
  
 以下部分中的信息特定于 Windows 防火墙。 您可以通过在命令提示符处运行命令或在“Windows 防火墙”对话框中设置属性来配置 Windows 防火墙系统。  
  
 有关默认 Windows 防火墙设置的详细信息以及有关影响数据库引擎、Analysis Services、Reporting Services 和 Integration Services 的 TCP 端口的说明，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="configuring-a-windowsfirewall"></a>配置 Windows 防火墙  
 您可以使用下面的命令来打开 TCP 端口 135、向例外列表中添加 MsDtsSrvr.exe 以及指定防火墙不阻止的范围。  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>使用命令提示符窗口配置 Windows 防火墙  
  
1.  运行命令： `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  运行命令： `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  若要打开所有计算机的防火墙，同时打开 Internet 上的计算机的防火墙，请用 scope=ALL 代替 scope=SUBNET。  
  
 下面的步骤描述了如何使用 Windows 用户界面来打开 TCP 端口 135，向例外列表中添加 MsDtsSrvr.exe 并指定防火墙不阻止的范围。  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>使用“Windows 防火墙”对话框配置防火墙  
  
1.  在“控制面板”中，双击“Windows 防火墙”。  
  
2.  在 **“Windows 防火墙”** 对话框中，单击 **“例外”** 选项卡，再单击 **“添加程序”**。  
  
3.  在“添加程序”对话框中单击“浏览”，导航到 Program Files\Microsoft SQL Server\100\DTS\Binn 文件夹，单击 MsDtsSrvr.exe，然后单击“打开”。 单击 **“确定”** 关闭 **“添加程序”** 对话框。  
  
4.  在 **“例外”** 选项卡上，单击 **“添加端口”**。  
  
5.  在“添加端口”对话框中，键入 **RPC(TCP/135)** 或在“名称”框中键入另一个描述性名称，在“端口号”框中键入 **135**，然后选择“TCP”。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务始终使用端口 135。 您不能指定其他端口。  
  
6.  在 **“添加端口”** 对话框中，可以选择单击 **“更改范围”** 来修改默认的作用范围。  
  
7.  在“更改范围”对话框中，选择“我的网络（仅子网）”或键入自定义列表，然后单击“确定”。  
  
8.  若要关闭 **“添加端口”** 对话框，请单击 **“确定”**。  
  
9. 若要关闭 **“Windows 防火墙”** 对话框，请单击 **“确定”**。  
  
    > [!NOTE]  
    >  为了配置 Windows 防火墙，此过程使用“控制面板”中的 **“Windows 防火墙”** 项。 **“Windows 防火墙”** 项仅可为当前网络位置配置文件配置防火墙。 但你也可使用 **netsh** 命令行工具或名为高级安全 Windows 防火墙的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理控制台 (MMC) 管理单元来配置 Windows 防火墙。 有关这些工具的详细信息，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="see-also"></a>请参阅  
 [配置 Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)   
 [Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)  
  
  
