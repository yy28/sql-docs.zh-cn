---
title: 要开始使用云中的 SQL Server 2017 |Microsoft 文档
description: 本快速入门演示如何在 Linux 中的所选云上运行 SQL Server 2017。
author: annashres
ms.author: annashres
manager: craigg
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.openlocfilehash: 29ed2b218f4d9c746f9356a2a57bbacd845b4df6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="quickstart-run-the-sql-server-2017-in-the-cloud"></a>快速入门： 在云中运行 SQL Server 2017

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入门教程，你将 Red Hat Enterprise Linux (RHEL)、 SUSE Linux 企业服务器 (SLES) 或在所选的云中的 Ubuntu 上安装 SQL Server 自 2017 年。 转到[设置 Linux SQL Server 虚拟机在 Azure 门户](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)在 Azure 中的 Linux 上运行 SQL Server。

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Amazon Web 服务
1.  在至少具有 2 GB 的内存来自应用商店创建 Linux AMI 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  连接到与 AMI ssh
1.  按照你选择的 Linux 分发的快速入门： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  为远程连接配置： 
    * 打开[Amazon EC2 控制台]( https://console.aws.amazon.com/ec2/)
    * 在导航窗格中，选择**安全组**。 
    * 选择**的入站、 编辑、 添加规则**
    * 添加入站的规则以允许 SQL Server 在其侦听 （默认 TCP 端口 1433年） 的端口上的流量

    
## <a name="digital-ocean"></a>数字海洋
1. 登录到[控制面板](https://cloud.digitalocean.com/login)单击创建快捷批处理
1. 选择 Ubuntu 16.04 快捷批处理在至少具有 2 GB 的内存
1. 连接到与快捷批处理 ssh
1. 请按照[Ubuntu 快速入门](quickstart-install-connect-ubuntu.md)
1. 为远程连接配置：
    * 在控制面板的顶部，请按照**网络**链接，然后选择**防火墙**
    * 添加入站的规则以允许 SQL Server 在其侦听 （默认 TCP 端口 1433年） 的端口上的流量
    
## <a name="google-cloud-platform"></a>Google 云平台
1.  在至少具有 2 GB 的内存从云启动器创建 Linux 映像 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  连接到的映像与 ssh
1.  按照你选择的 Linux 分发的快速入门： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  为远程连接配置： 
    * 转到[防火墙规则](https://console.cloud.google.com/networking/firewalls)
    * 添加入站的规则以允许 SQL Server 在其侦听的端口上的流量 (默认 tcp: 1433年)
