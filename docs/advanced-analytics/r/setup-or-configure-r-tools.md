---
title: "SQL Server 安装程序中包含的 R 工具 |Microsoft 文档"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9090313eed0997ea03329338c358825932dd8379
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="r-tools-included-with-sql-server-setup"></a>SQL Server 安装程序中包含的 R 工具

当与 SQL Server 安装 R 时，可以使用任何安装的相同 R 工具**基**R，如 RGui、 Rterm，等的安装。 因此从技术上讲，你具有所需开发和测试 R 代码的所有工具。

本主题列出了安装中包括的工具。

> [!TIP]
> 
> 通常是更轻松地调试和测试 R 代码，即使用专用的开发环境。 你将找到更轻松地在 SQL Server 中运行 R 代码，如果你事先在中测试它的外部工具，以便你可以阅读详细的错误消息和调试解决方案。
> 
> 请参阅本文列表可用于开发 R 解决方案，以及如何将它们配置为使用 SQL Server 的免费工具：[设置数据科学客户端](set-up-a-data-science-client.md)

**适用于：** SQL Server 2016 R Services （数据库） 和 Microsoft R Server （独立）;SQL Server 自 2017 年 1 机器学习服务 （数据库） 和机器学习 Server （独立）

## <a name="r-tools-included-with-installation"></a>包括与安装的 R 工具

以下标准 R 工具都将纳入*基本安装*，因此默认情况下安装。

+ **RTerm**： 用于运行 R 脚本的命令行终端

+ **RGui.exe**：适用于 R 的简单交互式编辑器。RGui.exe 和 RTerm 的命令行参数相同。

+ **RScript**：用于以批处理模式运行 R 脚本的命令行工具。

若要找到这些工具，确定设置 SQL Server 或独立机器学习功能一起安装的 R 库。 例如，在默认安装中，R 工具位于以下文件夹：

+ SQL Server 2016 R Services:`~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server 独立：`~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 自 2017 年 1 机器学习服务：`~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ 机器学习 Server （独立）：`~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

如果你需要使用 R 工具的帮助，只需打开**RGui**，单击**帮助**，然后选择其中一个选项。

## <a name="introducing-microsoft-r-client"></a>引入 Microsoft R 客户端

Microsoft R 客户端是一个免费下载，使你可以访问的开发使用 RevoScaleR 包。 通过安装 R 客户端，你可以创建可以在所有受支持的计算上下文，包括 SQL Server 数据库中分析和分布式 R 计算 Hadoop、 Spark 中或使用机器学习服务器的 Linux 上运行的 R 解决方案。

如果你已安装不同的 R 开发环境，如 RStudio，一定要重新配置要使用的库和可执行文件由 Microsoft R 客户端提供的环境。 通过这样你可以使用 RevoScaleR 包的所有功能尽管性能将受到限制。

有关详细信息，请参阅[什么是 Microsoft R 客户端？](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)
