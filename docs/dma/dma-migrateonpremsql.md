---
title: 使用数据迁移助手 SQL Server 升级
description: 了解如何使用数据迁移助手将本地 SQL Server 升级到 SQL Server 的更高版本或 Azure Vm 上的 SQL Server
ms.custom: seo-lt-2019
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: fc78354e3b422342e376bd7ebe75233dcd3ffaee
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056533"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>使用数据迁移助手 SQL Server 升级

数据迁移助手提供对本地 SQL Server 的无缝评估，并可升级到 Azure Vm 或 Azure SQL 数据库上的 SQL Server 或 SQL Server 迁移到更高版本。

本文提供了有关将 SQL Server 本地升级到更高版本 SQL Server 或使用数据迁移助手在 Azure Vm 上 SQL Server 的分步说明。

## <a name="create-a-new-migration-project"></a>创建新的迁移项目

1. 在左侧窗格中，选择 "**新建**（+）"，然后选择 "**迁移**" 项目类型。

2. 如果要将本地 SQL Server 升级到本地 SQL Server 的更高版本，请将源和目标服务器类型设置为**SQL Server** 。

3. 选择“创建”。

   ![创建迁移项目](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定源和目标

1. 对于 "源"，请在 "**源服务器详细信息**" 部分的 "**服务器名称**" 字段中输入 SQL Server 实例名称。 

2. 选择源 SQL Server 实例支持的**身份验证类型**。

3. 对于目标，请在 "**目标服务器详细信息**" 部分的 "**服务器名称**" 字段中输入 SQL Server 实例名称。 

4. 选择目标 SQL Server 实例支持的**身份验证类型**。

5. 建议你通过在 "**连接属性**" 部分中选择 "**加密连接**" 来加密连接。

6. 系统提示您启用数据连接时单击 **“下一步”** 。

   ![指定源和目标页](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>添加数据库

1. 仅在 "**添加数据库**" 页的左窗格中选择要迁移的特定数据库。

   默认情况下，选择源 SQL Server 实例上的所有用户数据库进行迁移

2. 通过执行以下操作，使用页面右侧的 "迁移设置" 设置应用于数据库的迁移选项。

   > [!NOTE]
   > 通过在左窗格中选择服务器，可以将迁移设置应用于要迁移的所有数据库。 还可以通过在左窗格中选择数据库，使用特定的设置来配置单个数据库。

    A. 指定**用于备份操作的源和目标 SQL 服务器可访问的共享位置**。 请确保运行源 SQL Server 实例的服务帐户对共享位置具有写入权限，并且目标服务帐户对共享位置具有读取权限。

    b. 指定要在目标服务器上还原数据和事务日志文件的位置。

    !["添加数据库" 页](../dma/media/AddDatabases.png)

3. 在 "**共享位置" 选项**框中输入源和目标 SQL Server 实例有权访问的共享位置。

4. 如果无法提供源和目标 SQL 服务器都可以访问的共享位置，请选择 "**将数据库备份复制到目标服务器可以读取和还原的其他位置**"。 然后，在 "**还原备份的位置" 选项**框中输入一个值。 

   请确保运行数据迁移助手的用户帐户对备份位置具有读取权限，并将权限写入目标服务器从中还原的位置。

   ![将数据库备份复制到不同位置的选项](../dma/media/CopyDatabaseDifferentLocation.png)

5. 选择“**下一步**”。

数据迁移助手对备份文件夹、数据和日志文件位置执行验证。 如果任何验证失败，请修复这些选项，然后选择 "**下一步**"。

## <a name="select-logins"></a>选择登录名

1. 选择要迁移的特定登录名。

   > [!IMPORTANT]
   > 请确保选择映射到选定要迁移的数据库中的一个或多个用户的登录名。   

   默认情况下，将为迁移选择符合迁移条件的所有 SQL Server 和 Windows 登录名。

2. 选择 "**开始迁移**"。

   ![选择登录名并开始迁移](../dma/media/SelectLogins.png)

## <a name="view-results"></a>查看结果

可以在 "**查看结果**" 页上监视迁移进度。

![查看结果页](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>导出迁移结果

1. 单击 "**查看结果**" 页底部的 "**导出报表**"，将迁移结果保存到 CSV 文件中。

2. 查看保存的文件以获取有关登录迁移的详细信息，然后验证所做的更改。

## <a name="see-also"></a>另请参阅

- [数据迁移助手（DMA）](../dma/dma-overview.md)
- [数据迁移助手：配置设置](../dma/dma-configurationsettings.md)
- [数据迁移助手：最佳实践](../dma/dma-bestpractices.md)
