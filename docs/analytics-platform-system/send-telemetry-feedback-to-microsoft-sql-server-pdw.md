---
title: 遥测数据的反馈-分析平台系统 |Microsoft Docs
description: Analytics Platform system 向 Microsoft 发送遥测反馈。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 442505d470d1c7b7a82a02610d650d9f0b8c8d07
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591134"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Analytics Platform system 向 Microsoft 发送遥测反馈
分析平台系统具有一个可选的遥测功能，将管理控制台数据发送到 Microsoft。 
  
> [!NOTE]  
> 在此版本中，Microsoft 不主动监视遥测数据。 是仅用于分析所收集的数据。  
  
## <a name="privacy"></a>隐私  
若要提供最大的隐私保护，AP 提供而不启用遥测。 启用此功能前，首先请查看[Microsoft 分析平台系统隐私声明](https://go.microsoft.com/fwlink/?LinkId=400902)。 若要选择加入，请运行如下所述的 PowerShell 脚本。  
  
## <a name="enable"></a>启用遥测  
**DNS 转发：** 向 Microsoft 发送遥测数据需要 Analytics Platform System 能够连接到 DNS 转发器通过 internet 进行访问。 若要启用此功能，必须启用 DNS 转发所有主机和工作负荷 Vm 上。 调用`Enable-RemoteMonitoring`命令与`SetupDnsForwarder`选项来正确配置 DNS 转发并启用遥测。 调用`Enable-RemoteMonitoring`命令而无需`SetupDnsForwarder`选项已配置 DNS 转发并且只想要启用检测信号监视时。  
  
> [!IMPORTANT]  
> 启用 DNS 转发打开所有主机和工作负荷 Vm 的 internet 的连接。  
  
#### <a name="to-enable-feedback"></a>若要启用的反馈  
  
1.  使用设备的域管理员帐户，连接到控制节点 (<strong>*appliance_domain*-CTL01</strong>)，然后打开命令提示符下使用你的 Windows 管理员凭据。  
  
2.  导航到以下目录： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  导入模块 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要导入你必须在命令中使用两个句点。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  调用`Enable-RemoteMonitoring`命令。  
  
    > [!NOTE]  
    > 该脚本假设 internet 连接工作正常，并且不会验证 internet 连接。  
  
    1.  首次启用遥测数据，使用以下命令以确保正确配置所有 DNS 转发器。 在此示例中的 DNS 转发 IP 地址替换`xx.xx.xx.xx`与您的环境中的 DNS 转发器 IP 地址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  当已配置 DNS 转发器，如重新启用以前禁用的遥测数据时，使用以下命令来启用遥测数据，而配置 DNS 转发时可用。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  系统将提示您阅读并认可 APS 将收集有关设备信息。 将 AP 隐私声明可以复制并粘贴到查看任何 internet 浏览器的链接。  
  
6.  输入**Y**以接受和反馈中选择或输入**N**不接受。  
  
7.  如果您输入**Y**将有一系列的命令将运行，这将启用遥测数据 （和可选 DNS 转发器） 在你的设备上的功能。 如果看到任何错误或让你相信该命令未成功的信息联系 CSS 寻求帮助。  
  
如果您输入**N**、 将运行任何命令并将不会启用该功能和不包含任何内容，以便执行操作。  
  
不没有运行任何危害`Enable-RemoteMonitoring`命令多次。 如果已设置 DNS 转发器，则将获取一条警告消息，指示这种情况。  
  
## <a name="disable"></a>禁用遥测  
禁用遥测数据将停止所有操作用于传达有关监视云服务的 AP 到设备的状态信息。  
  
> [!IMPORTANT]  
> 执行此操作不会禁用你的 DNS 转发器或 internet 连接，这可能正在使用的设备中的其他功能。  
  
#### <a name="to-disable-telemetry"></a>若要禁用遥测  
  
1.  使用设备的域管理员帐户，连接到控制节点 (<strong>*appliance_domain*-CTL01</strong>)，并使用管理员权限打开 PowerShell 窗口。  
  
2.  导航到以下目录： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  导入模块 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要导入你必须在命令中使用两个句点。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  调用`Disable-RemoteMonitoring`不带参数的命令。 此命令将停止发送反馈。 （这不会影响本地监视。）但是，该命令将不禁用 DNS 转发器和/或禁用任何 internet 连接。 这必须手动完成后已成功禁用反馈。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果看到任何错误或让你相信该命令未成功的信息联系 CSS 寻求帮助。  
  
不没有运行任何危害`Disable-RemoteMonitoring`命令多次。  
  
## <a name="next-steps"></a>后续步骤
有关详细信息，请参阅：
- [通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [使用系统视图监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-views.md)  
- [使用 System Center Operations Manager 监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [使用 DNS 转发器解析非设备 DNS 名称&#40;分析平台系统&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
