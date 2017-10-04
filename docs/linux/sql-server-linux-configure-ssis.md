---
title: "使用 ssis conf 在 Linux 上配置 SSIS |Microsoft 文档"
description: "这篇文章演示如何使用 ssis conf 实用程序在 Linux 上配置 SQL Server Integration Services。"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 46327772e8c22f76770bc51f72817ceedffae469
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>使用 ssis conf 在 Linux 上配置 SQL Server Integration Services

`ssis-conf`是一个配置脚本时，为 Red Hat Enterprise Linux 和 Ubuntu 安装 SQL Server Integration Services (SSIS)。 此实用程序可用于配置以下属性：

| Command | Description |
|-------------|---------------------------------------------------------------------|
| 集版本 | 设置 SQL Server 的版本                                       |
| 遥测   | 启用或禁用 SQL Server Integration Services 遥测服务 |
| 安装       | 初始化并设置 Microsoft SQL Server Integration Services      |
|||

## <a name="how-to-run-ssis-conf"></a>如何运行 ssis conf

运行这篇文章中的示例`ssis-conf`通过指定的完整路径： `/opt/ssis/bin/ssis-conf`。 如果您导航到该路径在运行之前`ssis-conf`，你可以在当前目录的上下文中运行该实用程序： `./ssis-conf`。

请确保运行以根用户权限本文中所述的命令。 例如，运行`sudo /opt/ssis/bin/ssis-conf setup`而不`/opt/ssis/bin/ssis-conf setup`。

若要运行这些命令中需要的语言的提示，你可以指定区域设置。 例如，若要查看中文的提示，请运行以下命令：

`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>使用组-版本来设置 SQL Server Integration Services 的版本

SSIS 的版本的 SQL Server 版本与对齐。

输入以下命令：

`$ sudo /opt/ssis/bin/ssis-conf set-edition`

输入命令后，你将看到以下提示：

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

Details about editions can be found at

https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409

Use of PAID editions of this software requires separate licensing through a

Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate

number of licenses in place to install and run this software.

Enter your edition(1-8):
```

如果输入介于 1 和 7 之间的一个值，系统配置是免费还是付费版本。 如果输入 8，该实用工具会提示你输入您购买的产品密钥：

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>使用遥测来配置客户反馈

`telemetry`命令确定 SSIS 是否向 Microsoft 发送反馈。

对于免费版本 （即，Express、 Developer 和 Evaluation 版本），遥测服务始终处于启用状态。 如果你具有免费版，则无法使用`telemetry`命令以禁用遥测。

输入以下命令：

`$ sudo /opt/ssis/bin/ssis-conf telemetry`

对于付费版本，你输入命令之后, 你将看到以下提示：

```
Send feature usage data to Microsoft. Feature usage data includes information
about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

如果选择**是**，遥测服务已启用，然后开始运行。 服务自动-启动后每个启动。 如果选择**否**，遥测服务停止，并且已禁用。

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>使用安装程序初始化并设置 Microsoft SQL Server Integration Services

使用`setup`命令每次安装 SSIS。

输入以下命令：

`sudo /opt/ssis/bin/ssis-conf setup`

该实用工具会提示你确认或对以下各项提供值：
-   产品许可证
-   EULA 协议
-   遥测服务
-   Integration Services 使用的语言

若要运行`setup`命令提示的语言与您希望在你可以指定区域设置。 例如，若要查看中文的提示，运行以下命令： `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="ssisconf-format"></a>ssis.conf 格式

以下`/var/opt/ssis/ssis.conf`文件提供了为每个设置的一个示例。

对于 SQL Server，你可以通过更改中的值更改系统设置`mssql.conf`文件。 SSIS，为你**无法**通过更改中的值来更改系统设置`ssis.conf`文件。 `ssis.conf`文件仅显示安装程序的结果。 如果你想要更改 SSIS 的设置，则可以删除`ssis.conf`文件，运行`setup`试命令。

下面是一个示例`ssis.conf`文件。 每个字段对应于一个安装程序步骤的结果。

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
