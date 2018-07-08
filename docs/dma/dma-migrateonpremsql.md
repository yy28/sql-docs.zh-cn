---
title: 将使用数据迁移助手的本地 SQL Server 迁移 |Microsoft Docs
description: 了解如何使用数据迁移助手将本地 SQL Server 迁移到另一个 SQL Server 或 Azure SQL 数据库
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 8133b4176fc8f8197cab646d51f4ece68b6250bc
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37784808"
---
# <a name="migrate-an-on-premises-sql-server-with-data-migration-assistant"></a>将使用数据迁移助手的本地 SQL Server 迁移

本文提供使用数据迁移助手迁移 SQL Server 的分步说明。 数据迁移助手提供无缝的评估和迁移到新式的本地 SQL Server 和 SQL Azure VM 数据平台和 Azure SQL 数据库。  

若要执行迁移，请完成以下任务。

- [创建新的迁移项目](#create-a-new-migration-project)
- [指定的源和目标](#specify-source-and-target)
- [添加数据库](#add-databases)
- [选择登录名](#select-logins)

## <a name="create-a-new-migration-project"></a>创建新的迁移项目

1. 单击**新建**（+） 左窗格中，然后选择**迁移**项目类型。

1. 将源和目标服务器类型设置为**SQL Server**如果正在升级到的本地 SQL Server 了新式的本地 SQL Server。

1. 单击 **“创建”**。

   ![创建迁移项目](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定的源和目标

1. 对于源中，输入中的 SQL Server 实例名称**服务器名称**字段中**源服务器的详细信息**部分。 

1. 选择**身份验证类型**受源 SQL Server 实例。

1. 对于目标，输入中的 SQL Server 实例名称**服务器名称**字段中**目标服务器详细信息**部分。 

1. 选择**身份验证类型**受目标 SQL Server 实例。

1. 建议通过选择加密连接**对连接进行加密**中**连接属性**部分。

1. 单击“下一步” 。

   ![指定源和目标页](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>添加数据库

1. 选择你想要只在左窗格中选择这些数据库，迁移的特定数据库**将数据库添加**页。

   默认情况下为进行迁移选择源 SQL Server 实例上的所有用户数据库

1. 使用页面右侧的迁移设置设置将应用于数据库中，通过执行以下迁移选项。

   > [!NOTE]
   > 您可以将迁移设置应用于要迁移，通过在左窗格中选择服务器的所有数据库。 通过在左窗格中选择数据库，还可以使用特定的设置配置单独的数据库。

 1. 指定**由备份操作的源和目标 SQL 服务器共享位置访问**。 请确保运行源的服务帐户 SQL Server 实例具有写入权限的共享位置和目标服务帐户具有读取共享位置上的权限。

 1. 指定要还原的数据和目标服务器上的事务日志文件的位置。

    ![添加数据库页](../dma/media/AddDatabases.png)

1. 输入源和目标 SQL Server 实例具有访问权限，在共享的位置**共享位置选项**框。

1. 如果您不能提供的共享的位置的源和目标 SQL Server 有权，请选择**将数据库备份复制到目标服务器可以读取和从还原的不同位置**。 然后，输入一个值**的还原选项的备份位置**框。 

   请确保运行数据迁移助手的用户帐户具有读取权限的备份位置，并写入到目标服务器将还原的位置的权限。

   ![若要将数据库备份复制到不同位置的选项](../dma/media/CopyDatabaseDifferentLocation.png)

1. 单击“下一步” 。

数据迁移助手会执行验证备份的文件夹中，数据和日志文件位置。 如果任何验证失败，请修复该选项并单击**下一步**。

## <a name="select-logins"></a>选择登录名

1. 选择用于迁移的特定登录名。

   > [!IMPORTANT]
   > 请务必选择映射到选择用于迁移的数据库中的一个或多个用户的登录名。   

   默认情况下，为进行迁移选择符合迁移条件的所有 SQL Server 和 Windows 登录名。

1. 单击**开始迁移**。

   ![选择登录名，并开始迁移](../dma/media/SelectLogins.png)

## <a name="view-results"></a>查看结果

可以监视迁移进度**查看结果**页。

![视图结果页](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>导出迁移结果

1. 单击**将报表导出**底部**查看结果**页后，可以将迁移结果保存到 CSV 文件。

1. 查看已保存的文件以获取有关登录名迁移的详细信息，然后验证所做的更改。

## <a name="see-also"></a>另请参阅

[数据迁移助手 (DMA)](../dma/dma-overview.md)

[数据迁移助手： 配置设置](../dma/dma-configurationsettings.md)

[数据迁移助手： 最佳实践](../dma/dma-bestpractices.md)
