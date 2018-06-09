---
title: 数据迁移助手 (SQL Server) 概述 |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: dd681a6445c6759b0ec17e06dc0b4dbf24b3b72f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707965"
---
# <a name="overview-of-data-migration-assistant"></a>数据迁移助手的概述

数据迁移助手 (DMA) 使您能够通过检测可能会影响你的 SQL Server 和 Azure SQL 数据库的新版本中的数据库功能的兼容性问题升级到现代数据平台。 DMA 性能和你的目标环境的可靠性改进建议，并允许你将架构、 数据和非包含的对象从源服务器移到目标服务器。

> [!NOTE] 
> 对于大型 （在方面的数量和大小数据库） 迁移，建议使用[Azure 数据库迁移服务](https://docs.microsoft.com/azure/dms/dms-overview)，这将在规模较大的数据库迁移。
  
## <a name="capabilities"></a>功能

- 评估迁移到 Azure SQL 数据库的本地 SQL Server 实例。 评估工作流帮助可以检测到可能会影响 Azure SQL 数据库迁移，并提供有关如何解决这些问题的详细的指南的以下问题。

  - 迁移阻塞问题： 发现兼容性问题，块迁移的本地 SQL Server 数据库到 Azure SQL 数据库 s。 DMA 提供建议，以帮助你解决这些问题。

  - 部分支持或不受支持的功能： 检测到当前正在使用源 SQL Server 实例上的部分支持或不受支持的功能。 DMA 提供一套全面的建议，在 Azure 中和缓解措施中可用的其他方法，以便你可以将合并到你迁移的项目。

- 发现可能会影响到本地 SQL Server 升级的问题。 这些被称为兼容性问题，而且必须组织在以下类别：

  - 重大更改
  - 行为更改
  - 已弃用的功能

- 发现数据库可以受益于升级后的目标 SQL Server 平台中的新增功能。 这些被称为功能建议和分为以下类别：

  - “性能”
  - Security
  - 存储器

- 将本地 SQL Server 实例迁移到托管在本地或 Azure 虚拟机 (VM)，可从你的本地网络访问的现代 SQL Server 实例。 可以使用 VPN 或其他技术访问 Azure VM。 迁移工作流可帮助你迁移以下组件：

  - 数据库的架构
  - 数据和用户
  - 服务器角色
  - SQL Server 和 Windows 登录名

- 成功迁移之后，应用程序可以连接到目标 SQL server 数据库无缝。

## <a name="supported-source-and-target-versions"></a>支持的源和目标版本

DMA 替换所有以前版本的 SQL Server 升级顾问，并应该用于大多数 SQL Server 版本的升级。 按照支持的源和目标版本。

**源**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- Windows 版 SQL Server 2017

**目标**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- 在 Windows 和 Linux 上的 SQL Server 自 2017 年 1
- Azure SQL Database

> [!NOTE] 
> DMA 当前不支持 Azure SQL 数据库托管实例作为目标。

## <a name="installation"></a>安装

若要安装 DMA，下载最新版本中的工具[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595)，然后运行**DataMigrationAssistant.msi**文件。

## <a name="see-also"></a>另请参阅

[评估你的 SQL Server 迁移](../dma/dma-assesssqlonprem.md)

[数据迁移助手： 配置设置](../dma/dma-configurationsettings.md)

[迁移在本地 SQL Server 使用数据迁移助手](../dma/dma-migrateonpremsql.md)

[数据迁移助手： 最佳实践](../dma/dma-bestpractices.md)



