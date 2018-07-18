---
title: 开始使用云中的 SQL Server 2017 |Microsoft Docs
description: 本快速入门介绍如何在 Linux 中所选云上运行 SQL Server 2017。
author: annashres
ms.author: annashres
manager: craigg
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: f5d67ff25cb5d2816672fafe0602d56921c034bb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37995886"
---
# <a name="quickstart-run-the-sql-server-2017-in-the-cloud"></a>快速入门： 在云中运行 SQL Server 2017

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在此快速入门中，您将 Red Hat Enterprise Linux (RHEL)、 SUSE Linux Enterprise Server (SLES) 或所选的云环境中的 Ubuntu 上安装 SQL Server 2017。 转到[预配 Linux SQL Server 虚拟机在 Azure 门户中](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)在 Azure 中的 Linux 上运行 SQL Server。

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Amazon Web 服务
1.  使用至少 2 GB 的内存从 marketplace 中创建 Linux AMI 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Ssh 连接到与 AMI
1.  按照所选的 Linux 分发版快速入门： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  为远程连接配置： 
    * 打开[Amazon EC2 控制台]( https://console.aws.amazon.com/ec2/)
    * 在导航窗格中，选择**安全组**。 
    * 选择**入站、 编辑、 添加规则**
    * 添加入站的规则以允许 SQL Server 侦听的端口 （默认 TCP 端口 1433年） 上的流量

    
## <a name="digital-ocean"></a>Digital Ocean
1. 登录到[控制面板](https://cloud.digitalocean.com/login)，然后单击创建快捷批处理
1. 选择 Ubuntu 16.04 快捷批处理具有至少 2 GB 内存
1. Ssh 连接到与水滴
1. 请按照[Ubuntu 快速入门](quickstart-install-connect-ubuntu.md)
1. 为远程连接配置：
    * 在控制面板的顶部，请按照**联网**链接，然后选择**防火墙**
    * 添加入站的规则以允许 SQL Server 侦听的端口 （默认 TCP 端口 1433年） 上的流量
    
## <a name="google-cloud-platform"></a>Google 云平台
1.  创建具有至少 2 GB 的内存从云启动器的 Linux 映像 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  连接到的映像与 ssh 配合使用
1.  按照所选的 Linux 分发版快速入门： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  为远程连接配置： 
    * 转到[防火墙规则](https://console.cloud.google.com/networking/firewalls)
    * 添加入站的规则以允许 SQL Server 在其侦听的端口上的流量 (默认 tcp: 1433年)
