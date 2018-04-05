---
title: 迁移在本地 SQL Server （数据迁移助手） |Microsoft 文档
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql-non-specified
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
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 666236842318cfba0cee38f71ac694eef86cdbf5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="migrate-on-premises-sql-server-using-data-migration-assistant"></a>迁移在本地 SQL Server 使用数据迁移助手

这篇文章提供有关迁移的 SQL Server 的分步说明，使用数据迁移助手。

数据迁移助手提供无缝的评估和迁移到现代的在本地 SQL Server 和 SQL Azure VM 数据平台。  

完成以下任务来执行迁移。

- [创建新的迁移项目](#create-a-new-migration-project)
- [指定的源和目标](#specify-source-and-target)
- [添加数据库](#add-databases)
- [选择登录名](#select-logins)

## <a name="create-a-new-migration-project"></a>创建新的迁移项目

1. 单击**新建**（+） 上的左窗格中和选择**迁移**项目类型。

1. 将源和目标服务器类型设置为**SQL Server**如果你要升级到 SQL Server 的本地现代本地 SQL Server。

1. 单击 **“创建”**。

   ![创建迁移项目](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定的源和目标

1. 对于源中，输入中的 SQL Server 实例名称**服务器名称**字段**源服务器的详细信息**部分。 

1. 选择**身份验证类型**受源 SQL Server 实例。

1. 目标中输入中的 SQL Server 实例名称**服务器名称**字段**目标服务器详细信息**部分。 

1. 选择**身份验证类型**受目标 SQL Server 实例。

1. 建议您通过选择加密连接**加密连接**中**连接属性**部分。

1. 单击“下一步” 。

   ![指定源和目标页](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>添加数据库

1. 选择你想要通过仅在左窗格中选择这些数据库，迁移的特定数据库**将数据库添加**页。

   默认情况下选择迁移源 SQL Server 实例上的所有用户数据库

1. 使用页面右侧的迁移设置设置将应用于数据库中，通过执行以下迁移选项。

   > [!NOTE]
   > 可以将迁移设置应用到你要进行迁移，通过在左窗格中选择的服务器的所有数据库。 通过在左窗格中选择数据库，还可以配置单个数据库具有特定设置。


 1. 指定**由备份操作的源和目标 SQL server 共享可访问位置**。 请确保运行源的服务帐户 SQL Server 实例具有写入权限的共享位置和目标服务帐户具有读取权限的共享位置。

 1. 指定要还原的数据和目标服务器上的事务日志文件的位置。

    ![添加数据库页](../dma/media/AddDatabases.png)

1. 输入源和目标 SQL Server 实例，可以访问的在共享的位置**共享位置选项**框。

1. 如果你不能提供的共享的位置的源和目标的 SQL 服务器有权，选择**将数据库备份复制到目标服务器可读取和从还原的不同位置**。 然后，输入一个值**备份来还原选项备份位置**框。 

   请确保运行数据迁移助手的用户帐户具有读取权限的备份位置，并写入到目标服务器将还原的位置的权限。

   ![选项可将数据库备份复制到其他位置](../dma/media/CopyDatabaseDifferentLocation.png)

1. 单击“下一步” 。

数据迁移助手会执行验证对备份的文件夹，数据和日志文件位置。 如果任何验证失败，请修复该选项，然后单击**下一步**。

## <a name="select-logins"></a>选择登录名

1. 选择用于迁移的特定登录名。

   > [!IMPORTANT]
   > 请确保选择映射到选择要迁移的数据库中的一个或多个用户的登录名。   

   默认情况下，迁移被选择符合迁移条件的所有 SQL Server 和 Windows 登录名。

1. 单击**开始迁移**。

   ![选择登录名，并开始迁移](../dma/media/SelectLogins.png)

## <a name="view-results"></a>查看结果

你可以通过监视迁移进度**查看结果**页。

![视图结果页](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>导出迁移结果

1. 单击**导出报表**底部**查看结果**页后，可以将迁移结果保存到 CSV 文件。

1. 查看有关登录名迁移的详细信息的已保存的文件，然后确认所做的更改。

## <a name="see-also"></a>另请参阅

[数据迁移助手 (DMA)](../dma/dma-overview.md)

[数据迁移助手： 配置设置](../dma/dma-configurationsettings.md)

[数据迁移助手： 最佳实践](../dma/dma-bestpractices.md)
