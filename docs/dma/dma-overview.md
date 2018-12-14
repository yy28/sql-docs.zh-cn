---
title: 概述数据迁移助手 (SQL Server) |Microsoft Docs
description: 了解如何使用数据迁移助手将 SQL Server 数据库迁移到其他 SQL Server 或 Azure 数据库
ms.custom: ''
ms.date: 11/26/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 7ea185bd40dc9477b00b91069fa0ce8d93986aa5
ms.sourcegitcommit: 98324d9803edfa52508b6d5d3554614d0350a0b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321613"
---
# <a name="overview-of-data-migration-assistant"></a>数据迁移助手概述
数据迁移助手 (DMA) 可帮助您将升级到现代数据平台检测可能会影响新版本的 SQL Server 或 Azure SQL 数据库中的数据库功能的兼容性问题。 DMA 建议性能和可靠性改进为目标环境，并允许您将架构、 数据和非包含的对象从源服务器移动到目标服务器。

> [!NOTE] 
> 对于大型迁移 （从数和数据库的大小），我们建议你使用[Azure 数据库迁移服务](/azure/dms/dms-overview)，这可以在规模较大的数据库迁移。
  
## <a name="get-data-migration-assistant"></a>获取数据迁移助手
若要安装 DMA，下载最新版本中的工具[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53595)，然后运行**DataMigrationAssistant.msi**文件。

## <a name="capabilities"></a>功能
- 评估的本地 SQL Server 实例迁移到 Azure SQL 数据库。 评估工作流可帮助你检测到以下问题，可能会影响 Azure SQL 数据库迁移，并提供有关如何解决这些问题的详细的指南。

  - 迁移阻塞问题： 发现阻止迁移到 Azure SQL 数据库的本地 SQL Server 数据库的兼容性问题。 DMA 提供建议来帮助你解决这些问题。

  - 部分支持或不受支持的功能： 检测到当前正在使用源 SQL Server 实例上的部分支持或不受支持的功能。 DMA 提供了一套综合的建议，在 Azure 中和缓解步骤中可用的替代方法，以便将它们合并在迁移项目中。

- 发现可能会影响到在本地 SQL Server 升级的问题。 这些描述为兼容性问题，并按以下类别进行组织：

  - 重大更改
  - 行为更改
  - 已弃用的功能

- 了解数据库可以受益于升级后在目标 SQL Server 平台中的新增功能。 这些被称为功能建议，并按以下类别进行组织：

  - 性能
  - 安全性
  - 存储

- 将本地 SQL Server 实例迁移到最新 SQL Server 托管实例的本地或 Azure 可从你的本地网络访问虚拟机 (VM) 上。 可使用 VPN 或其他技术访问 Azure VM。 迁移工作流可帮助你迁移以下组件：

  - 数据库的架构
  - 数据和用户
  - 服务器角色
  - SQL Server 和 Windows 登录名

- 成功迁移后，应用程序可以连接到目标 SQL Server 数据库无缝。

## <a name="prerequisites"></a>必要条件
若要运行一次评估，您必须是 SQL Server 的成员**sysadmin**角色。

## <a name="supported-source-and-target-versions"></a>支持的源和目标版本
DMA 替换所有以前版本的 SQL Server 升级顾问，应使用的大多数 SQL Server 版本升级。 支持的源和目标版本为：

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
- 在 Windows 和 Linux 上的 SQL Server 2017
- Azure SQL Database
- Azure SQL 数据库托管实例

## <a name="see-also"></a>请参阅
[评估 SQL Server 迁移](../dma/dma-assesssqlonprem.md)     
[数据迁移助手：配置设置](../dma/dma-configurationsettings.md)     
[使用数据迁移助手迁移的本地 SQL Server](../dma/dma-migrateonpremsql.md)     
[数据迁移助手：最佳做法](../dma/dma-bestpractices.md)     
