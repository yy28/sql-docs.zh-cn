---
title: 数据迁移助手（SQL Server）概述 |Microsoft Docs
description: 了解如何使用数据迁移助手将 SQL Server 数据库迁移到其他 SQL Server 或 Azure 数据库
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 64c8416a15afd685559fe2d05c436c2e5fc1382d
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632850"
---
# <a name="overview-of-data-migration-assistant"></a>数据迁移助手概述

数据迁移助手（DMA）通过检测可能会影响新版本 SQL Server 或 Azure SQL 数据库中的数据库功能的兼容性问题，帮助升级到现代数据平台。 DMA 为目标环境建议性能和可靠性，并使你能够将架构、数据和非包含对象从源服务器移动到目标服务器。

> [!NOTE]
> 对于大型迁移（就数据库数量和大小而言），建议使用[Azure 数据库迁移服务](/azure/dms/dms-overview)，该服务可以大规模迁移数据库。
  
## <a name="get-data-migration-assistant"></a>获取数据迁移助手

若要安装 DMA，请从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53595)下载最新版本的工具，然后运行**DataMigrationAssistant**文件。

## <a name="capabilities"></a>功能

- 评估迁移到 Azure SQL 数据库的本地 SQL Server 实例。 评估工作流有助于检测可能影响 Azure SQL 数据库迁移的以下问题，并提供有关如何解决这些问题的详细指导。

  - 迁移阻止问题：发现阻止本地 SQL Server 数据库迁移到 Azure SQL 数据库的兼容性问题。 DMA 提供有助于解决这些问题的建议。

  - 部分支持或不支持的功能：检测当前在源 SQL Server 实例上使用的部分支持或不支持的功能。 DMA 提供一套全面的建议、Azure 中可用的替代方法和缓解步骤，使你能够将它们合并到你的迁移项目中。

- 发现可能会影响升级到本地 SQL Server 的问题。 它们被描述为兼容性问题，并按以下类别进行组织：

  - 重大更改
  - 行为更改
  - 已弃用的功能

- 发现目标 SQL Server 平台中的新功能，在升级后数据库可从中受益。 它们被描述为功能建议，并按下列类别进行组织：

  - 性能
  - 安全性
  - 存储器

- 将本地 SQL Server 实例迁移到在本地或从本地网络访问的 Azure 虚拟机（VM）上托管的新式 SQL Server 实例。 可以使用 VPN 或其他技术访问 Azure VM。 迁移工作流可帮助你迁移以下组件：

  - 数据库架构
  - 数据和用户
  - 服务器角色
  - SQL Server 和 Windows 登录名

- 成功迁移后，应用程序可以无缝地连接到目标 SQL Server 数据库。

- 评估迁移到 Azure SQL 数据库或 Azure SQL 数据库托管实例的本地 SQL Server Integration Services （SSIS）包。 评估有助于发现可能会影响迁移的问题。 它们被描述为兼容性问题，并按以下类别进行组织：

  - 迁移阻止程序：发现阻止将源包迁移到 Azure 的兼容性问题。 DMA 提供有助于解决这些问题的建议。

  - 信息问题：检测在源包中使用的部分支持或弃用的功能。

## <a name="prerequisites"></a>先决条件

若要运行评估，你必须是 SQL Server **sysadmin**角色的成员。

## <a name="supported-source-and-target-versions"></a>支持的源版本和目标版本

DMA 替换 SQL Server 升级顾问的所有早期版本，应将其用于升级大多数 SQL Server 版本。 支持的源版本和目标版本为：

**渠道**

- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows 上的 SQL Server 2017

**攻击**

- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows 和 Linux 上的 SQL Server 2017
- SQL Server 2019
- Azure SQL 数据库单一数据库
- Azure SQL 数据库托管实例
- 在 Azure 虚拟机上运行的 SQL server

## <a name="see-also"></a>另请参阅

[评估你的 SQL Server 迁移](../dma/dma-assesssqlonprem.md)

[数据迁移助手：配置设置](../dma/dma-configurationsettings.md)

[使用数据迁移助手迁移本地 SQL Server](../dma/dma-migrateonpremsql.md)

[数据迁移助手：最佳实践](../dma/dma-bestpractices.md)
