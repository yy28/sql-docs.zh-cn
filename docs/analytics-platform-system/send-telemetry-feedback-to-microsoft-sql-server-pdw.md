---
title: 遥测反馈
description: 针对分析平台系统将遥测反馈发送到 Microsoft。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400364"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>将遥测反馈发送给 Microsoft for Analytics 平台系统
分析平台系统具有可向 Microsoft 发送管理员控制台数据的可选遥测功能。 
  
> [!NOTE]  
> 在此版本中，Microsoft 不主动监视遥测数据。 出于分析目的，将收集数据。  
  
## <a name="privacy"></a><a name="privacy"></a>隐私  
为了提供最大的隐私保护，不启用遥测就提供了 AP。 在启用此功能之前，请先查看 [Microsoft Analytics Platform System 隐私声明](https://go.microsoft.com/fwlink/?LinkId=400902)。 若要选择加入，请运行下面所述的 PowerShell 脚本。  
  
## <a name="enable-telemetry"></a><a name="enable"></a>启用遥测  
**DNS 转发：** 向 Microsoft 发送遥测数据需要分析平台系统通过 DNS 转发器连接到 internet。 若要启用此功能，必须在所有主机和工作负荷 Vm 上启用 DNS 转发。 `Enable-RemoteMonitoring`使用选项调用命令 `SetupDnsForwarder` 以正确配置 DNS 转发并启用遥测。 `Enable-RemoteMonitoring` `SetupDnsForwarder` 如果已配置 DNS 转发并且你只希望启用检测信号监视，请在不使用选项的情况下调用命令。  
  
> [!IMPORTANT]  
> 启用 DNS 转发会打开适用于所有主机和工作负荷 Vm 的 internet 连接。  
  
#### <a name="to-enable-feedback"></a>启用反馈  
  
1.  使用设备域管理员帐户，连接到 Control 节点 (<strong> *appliance_domain*-CTL01</strong>) 并使用 Windows 管理员凭据打开命令提示符。  
  
2.  导航到以下目录： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 。  
  
3.  导入模块 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要导入，必须在命令中使用两个句点。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  调用 `Enable-RemoteMonitoring` 命令。  
  
    > [!NOTE]  
    > 此脚本假定 internet 连接正常工作，并且不会验证 internet 连接。  
  
    1.  第一次启用遥测时，请使用以下命令确保正确配置所有 DNS 转发器。 在此示例中，将 DNS 转发 IP 地址替换 `xx.xx.xx.xx` 为你的环境中的 Dns 转发器 ip 地址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  配置 DNS 转发器后，如重新启用以前禁用的遥测，请使用以下命令启用遥测，而不配置 DNS 转发。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  系统将提示你阅读并确认 AP 将收集有关设备的信息。 此时会出现一个指向 AP 隐私声明的链接，你可以将其复制并粘贴到任何 internet 浏览器中进行查看。  
  
6.  输入 **Y** 接受并选择加入反馈，或输入 **N** 以不接受。  
  
7.  如果输入 **Y** ，将会有一系列命令运行，这会使遥测 (和（可选）设备上的 DNS 转发器) 功能。 如果看到任何错误或信息，导致您认为该命令不能成功联系 CSS 以获得帮助。  
  
如果输入了 " **N**"，则不会运行任何命令，并且不会启用该功能，也不会对此进行任何其他操作。  
  
多次运行此命令不会有任何损害 `Enable-RemoteMonitoring` 。 如果已设置 DNS 转发器，将收到一条警告消息，指示这种情况。  
  
## <a name="disable-telemetry"></a><a name="disable"></a>禁用遥测  
禁用遥测将停止所有操作，这些操作将有关设备状态的信息传递到云中的 "AP 监视" 服务。  
  
> [!IMPORTANT]  
> 执行此操作将不会禁用你的 DNS 转发器或 internet 连接，因为设备中的其他功能可能正在使用该转发器或 internet 连接。  
  
#### <a name="to-disable-telemetry"></a>禁用遥测  
  
1.  使用设备域管理员帐户，连接到 Control 节点 (<strong> *appliance_domain*-CTL01</strong>) ，并使用管理员权限打开 PowerShell 窗口。  
  
2.  导航到以下目录： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 。  
  
3.  导入模块 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要导入，必须在命令中使用两个句点。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  调用 `Disable-RemoteMonitoring` 不带参数的命令。 此命令将停止发送反馈。  (这将不会影响本地监视。 ) 不过，该命令不会禁用 DNS 转发器和/或禁用任何 internet 连接。 成功禁用反馈后必须手动完成此操作。  
  
    **示例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果看到任何错误或信息，导致您认为该命令不能成功联系 CSS 以获得帮助。  
  
多次运行此命令不会有任何损害 `Disable-RemoteMonitoring` 。  
  
## <a name="next-steps"></a>后续步骤
有关详细信息，请参阅：
- [使用管理控制台 &#40;分析平台系统来监视设备&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [使用系统视图 &#40;分析平台系统来监视设备&#41;](monitor-the-appliance-by-using-system-views.md)  
- [使用 System Center Operations Manager &#40;Analytics 平台系统来监视设备&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [使用 DNS 转发器解析非设备 DNS 名称 &#40;分析平台系统&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
