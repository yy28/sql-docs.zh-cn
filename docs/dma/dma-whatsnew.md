---
title: 什么是数据迁移助手 (SQL Server) 中的新增功能 |Microsoft 文档
ms.custom: ''
ms.date: 02/02/2018
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0004406d86da4174898141d1f75c72186921b8d3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="whats-new-in-data-migration-assistant"></a>什么是数据迁移助手中的新增功能

本主题列出每个版本中添加的数据迁移助手 (DMA)。

## <a name="dma-v34"></a>DMA v3.4
DMA v3.4 版本还包括添加以下内容：
- 对 SQL Server 自 2017 年作为迁移到 Azure SQL 数据库的源的支持。
- 稳定性、 性能和评估规则正确性的增强功能。

## <a name="dma-v33"></a>DMA v3.3
DMA v3.3 版本，使迁移到新版本的 SQL Server 2017，Windows 和 Linux 上的本地 SQL Server 实例。 尽管 Windows 和 Linux 的总体迁移工作流是相同的适用于 Linux 迁移到 SQL Server 2017 需要几个其他注意事项。

### <a name="specifying-the-back-up-path"></a>指定的备份路径
Linux 和 Windows 使用不同的路径格式。 因此，迁移到在 Linux 上的 SQL Server 2017 要求用户提供 Windows 和 Linux 版本的物理文件的位置的路径。 具体取决于物理文件的位置不同的方式完成此操作。
如果运行的计算机上是物理的备份文件：
- Linux，请使用 samba 共享与网络上的其他计算机共享文件。
-   Windows 中，使用 mnt 命令来装载到运行 Linux 的计算机上共享。

> [!NOTE]
> 使用 samba 共享或 'mnt 命令的详细信息不在本文的讨论范围之内。

### <a name="migrating-windows-logins"></a>迁移 Windows 登录名
虽然在 Linux 上的 SQL Server 2017 正式支持的 Active Directory (AD) 登录迁移，但它需要额外配置才能正常工作。 请参阅主题[与在 Linux 上的 SQL Server 的 Active Directory 身份验证](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication)有关设置在 Linux 上的 SQL Server 2017 上的 Active Directory 登录名的详细信息。 此之后安装程序完成，你可以像往常一样将迁移 Active Directory 登录名。 标准 SQL 身份验证的工作与预期不进行任何附加设置。

## <a name="dma-v32"></a>DMA 3.2 版
DMA v3.2 版本还包括添加以下内容：

- 架构和数据迁移与新的迁移工作流启用从本地 SQL Server 数据库到 Azure SQL 数据库。

- 在架构迁移到 Azure SQL 数据库，DMA 脚本源数据库对象，提供有关如何解决任何潜在的兼容性问题的指导，然后将您的架构部署到 Azure。

## <a name="dma-v31"></a>DMA v3.1，解决
DMA v3.1，解决版本还包括添加以下内容：

- 在数据库排序规则方面的改进的评估建议的 Azure SQL 数据库使用的不受支持的系统存储过程和 CLR 对象。

- 兼容性级别 130、 120、 110，和 100 将迁移到 Azure SQL 数据库时的评估指南。

## <a name="dma-v30"></a>DMA v3.0
DMA v3.0 版本扩展 Azure SQL 数据库评估，以提供全面的建议，用于帮助解决与相关的问题：

- 迁移阻塞问题。

- 部分或不受支持的特性和功能。

## <a name="dma-v21"></a>DMA 2.1 版
DMA v2.1 版本还包括添加以下内容：
- 命令行支持在无人参与模式下，这有助于大规模运行评估运行评估。 有关更多详细信息，请参阅主题[运行数据迁移助手从命令行](dma-commandline.md)。

- 当用户启动和关闭 DMA 时的性能改进。

- 配置 SQL 连接超时的能力。有关更多详细信息，请参阅主题[数据迁移助手配置设置](dma-configurationsettings.md)。

## <a name="dma-v20"></a>DMA v2.0
DMA v2.0 版本包括改进的延伸数据库功能建议提供最大限度地节省的存储空间的正确按优先级排列的表。

## <a name="dma-v10"></a>DMA v1.0
DMA v1.0 发布，则初始版本中，并提供用于：
- 发现的问题可以影响升级到 SQL Server 的本地版本。 任何发现被称为兼容性问题，并分为以下几个方面：
    -   重大更改
    - 行为更改
    - 已弃用的功能

- 数据库可以受益于升级的目标 SQL Server 平台中的新功能的发现。 任何发现被称为功能建议和分为以下几个方面：
    - 性能
    - Security
    - 存储器

-   若要执行评估的现代用户体验。

## <a name="see-also"></a>另请参阅

[数据迁移助手的概述](../dma/dma-overview.md)
