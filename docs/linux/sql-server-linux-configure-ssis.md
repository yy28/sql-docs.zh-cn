---
title: 使用 ssis conf 配置 Linux 上的 SSIS |Microsoft Docs
description: 本文介绍如何使用 ssis conf 实用工具在 Linux 上配置 SQL Server Integration Services (SSIS)。
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 67144e934914549fbb2605b660407c826c409880
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020634"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>使用 ssis conf 配置 Linux 上的 SQL Server Integration Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在运行`ssis-conf`配置脚本时为 Red Hat Enterprise Linux 和 Ubuntu 安装 SQL Server Integration Services (SSIS)。 有关安装 SSIS 的详细信息，请参阅[安装 SQL Server Integration Services (SSIS) 在 Linux 上](sql-server-linux-setup-ssis.md)。

此外可以使用`ssis-conf`实用工具来配置以下属性：

| Command | Description |
|-------------|---------------------------------------------------------------------|
| 集版本 | 设置 SQL Server 版本                                       |
| 遥测数据   | 启用或禁用 SQL Server Integration Services 遥测服务 |
| 安装       | 初始化并设置 Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>运行 ssis conf

在本文中运行示例`ssis-conf`通过指定完整路径： `/opt/ssis/bin/ssis-conf`。 如果在运行之前导航到该位置`ssis-conf`，可以在当前目录的上下文中运行该实用工具： `./ssis-conf`。

请务必在本文中使用 root 权限运行命令所述。 例如，运行`sudo /opt/ssis/bin/ssis-conf setup`而不`/opt/ssis/bin/ssis-conf setup`。

若要运行这些命令使用你喜欢的语言中的提示，可以指定区域设置。 例如，若要在中文中会收到提示，运行以下命令： `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>使用集版本来设置版本的 SQL Server Integration Services

SSIS 的版本与 SQL Server 的版本。

输入以下命令： `$ sudo /opt/ssis/bin/ssis-conf set-edition`。

输入命令后，您将收到以下提示：

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

如果输入值从 1 到 7 时，系统将配置免费或付费版。 如果输入 8，该实用工具会提示您输入您购买的产品密钥：

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>使用遥测来配置客户反馈

`telemetry`命令确定 SSIS 是否向 Microsoft 发送反馈。

对于免费版本 （即，速成版、 开发人员版和评估版），始终启用遥测服务。 如果您有免费版本，则无法使用`telemetry`命令，以禁用遥测数据。

输入以下命令： `$ sudo /opt/ssis/bin/ssis-conf telemetry`。

对于付费版本，输入命令之后, 您将收到以下提示：

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

如果选择**是**，遥测服务已启用并开始运行。 每个启动后自动启动该服务。 如果选择**否**，遥测服务停止并已禁用。

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>使用安装程序初始化并设置 Microsoft SQL Server Integration Services

使用`setup`命令每次安装 SSIS 时。

输入以下命令： `sudo /opt/ssis/bin/ssis-conf setup`。

该实用工具会提示你确认或为以下各项提供值：
-   产品许可证
-   EULA 协议
-   遥测服务
-   Integration Services 使用的语言

若要运行`setup`命令提示在语言中，您愿意，可以指定区域设置。 例如，若要在中文中会收到提示，运行以下命令： `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="ssisconf-format"></a>ssis.conf 格式

以下`/var/opt/ssis/ssis.conf`文件提供每个设置的示例。

对于 SQL Server，可以通过更改中的值更改系统设置`mssql.conf`文件。 用于 SSIS，您*不能*通过更改中的值来更改系统设置`ssis.conf`文件。 `ssis.conf`文件显示了仅安装程序的结果。 如果你想要更改用于 SSIS 的设置，则可以删除`ssis.conf`文件，然后运行`setup`试命令。

下面是一个示例`ssis.conf`文件。 每个字段对应于一个安装步骤的结果。

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的相关的内容
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [限制和 Linux 上的 SSIS 的已知的问题](sql-server-linux-ssis-known-issues.md)
-   [计划 SQL Server Integration Services 包在 Linux 上的使用 cron 执行](sql-server-linux-schedule-ssis-packages.md)
