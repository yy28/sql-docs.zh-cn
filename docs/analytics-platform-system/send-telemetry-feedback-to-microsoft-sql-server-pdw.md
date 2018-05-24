---
title: 遥测反馈-分析平台系统 |Microsoft 文档
description: 分析平台系统向 Microsoft 发送遥测反馈。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 747274cd03e9cbd5dd2eab4423458700331358dd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>分析平台系统向 Microsoft 发送遥测反馈
分析平台系统具有一个可选的遥测功能，将管理控制台数据发送给 Microsoft。 
  
> [!NOTE]  
> 在此版本中，Microsoft 不主动监视的遥测数据。 仅用于分析收集数据。  
  
## <a name="privacy"></a>隐私  
若要提供最大的隐私保护，AP 附带而不启用遥测。 在之前启用此功能，首先查看[Microsoft 分析平台系统隐私声明](http://go.microsoft.com/fwlink/?LinkId=400902)。 若要选择加入，请运行如下所述的 PowerShell 脚本。  
  
## <a name="enable"></a>启用遥测  
**DNS 转发：** 向 Microsoft 发送遥测数据需要分析平台系统连接到在 internet 上通过 DNS 转发器。 若要启用此功能，必须启用转发所有主机和工作负荷 Vm 上的 DNS。 调用`Enable-RemoteMonitoring`命令`SetupDnsForwarder`选项正确配置 DNS 转发和启用遥测。 调用`Enable-RemoteMonitoring`命令而不`SetupDnsForwarder`选项在已配置 DNS 转发且你只想要启用检测信号监视。  
  
> [!IMPORTANT]  
> 启用 DNS 转发打开所有主机和工作负荷 Vm 的 internet 连接。  
  
#### <a name="to-enable-feedback"></a>若要启用反馈  
  
1.  使用设备的域管理员帐户，连接到管理节点 (***appliance_domain *-CTL01**)，然后打开命令提示符下使用您的 Windows 管理员凭据。  
  
2.  导航到以下目录： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  导入模块 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要导入你必须在命令中使用两个时间段。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  调用`Enable-RemoteMonitoring`命令。  
  
    > [!NOTE]  
    > 该脚本假设的 internet 连接工作正常，并且不会验证 internet 连接。  
  
    1.  启用遥测，首次使用以下命令以确保正确配置所有 DNS 转发器。 在此示例中的 DNS 转发 IP 地址替换`xx.xx.xx.xx`与你的环境中的 DNS 转发器 IP 地址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  当已配置 DNS 转发器，如重新启用以前已禁用遥测时，使用以下命令而不配置 DNS 转发启用遥测。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  系统将提示您读取并确认 AP 将收集有关设备的信息。 将可以复制并粘贴到查看任何 internet 浏览器的 AP 隐私声明的链接。  
  
6.  输入**Y**接受并反馈中选择或输入**N**为不接受。  
  
7.  如果你输入**Y**将一系列将运行这将启用遥测数据 （和可选 DNS 转发器） 的命令在你的设备上的功能。 如果你看到任何错误或引导你认为该命令未成功的信息请与 CSS 联系以获取帮助。  
  
如果你输入**N**将运行任何命令和将不会启用该功能，无需进行任何详细让您做什么。  
  
不没有运行任何影响`Enable-RemoteMonitoring`命令多次。 如果已设置 DNS 转发器，则你将获取一条警告消息，该值指示这种情况。  
  
## <a name="disable"></a>禁用遥测  
禁用遥测将停止所有操作用于传达有关监视服务在云中 AP 到设备的状态信息。  
  
> [!IMPORTANT]  
> 执行此操作不会禁用您的 DNS 转发器或 internet 连接，这可能是由设备中的其他功能使用。  
  
#### <a name="to-disable-telemetry"></a>若要禁用遥测  
  
1.  使用设备的域管理员帐户，连接到管理节点 (***appliance_domain *-CTL01**) 和使用管理员权限打开 PowerShell 窗口。  
  
2.  导航到以下目录： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  导入模块 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要导入你必须在命令中使用两个时间段。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  调用`Disable-RemoteMonitoring`命令不带参数。 此命令将停止发送反馈。 （这不会影响本地监视。）但是，该命令将不禁用 DNS 转发器和/或禁用任何 internet 连接。 这必须手动完成后成功禁用反馈。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果你看到任何错误或引导你认为该命令未成功的信息请与 CSS 联系以获取帮助。  
  
不没有运行任何影响`Disable-RemoteMonitoring`命令多次。  
  
## <a name="next-steps"></a>后续步骤
有关详细信息，请参阅：
- [通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [使用系统视图来监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-views.md)  
- [使用 System Center Operations Manager 来监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [使用 DNS 转发器来解析非设备 DNS 名称&#40;分析平台系统&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
