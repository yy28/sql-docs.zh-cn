---
title: 评估 SQL Server 数据资产迁移到 Azure SQL 数据库的准备情况 |Microsoft Docs
description: 了解如何使用数据迁移助手迁移 SQL Server 数据资产迁移到 Azure SQL 数据库
ms.custom: ''
ms.date: 07/16/2019
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
ms.author: rajpo
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269379"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>评估 SQL Server 数据资产迁移到 Azure SQL 数据库使用数据迁移助手的准备情况

迁移数百个 SQL Server 实例和数千个数据库到 Azure SQL 数据库，我们平台即服务 (PaaS) 产品/服务，需要相当长的执行。 若要简化尽可能多地过程，需要您进行迁移的相对就绪性更加自信。 标识成效，包括服务器和数据库完全准备好，或者要求最少的工作量以准备进行迁移，可简化并加速你的工作。

本文提供了分步说明有关利用[数据迁移助手](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017)进行汇总准备情况结果和在呈现它们[Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)中心。

## <a name="create-a-project-and-add-a-tool"></a>创建一个项目并添加工具

设置 Azure 订阅中的新 Azure Migrate 项目，然后添加一个工具。

Azure Migrate 项目用于存储发现、 评估和迁移从正在评估或迁移的环境收集的元数据。 跟踪已发现的资产并安排评估和迁移，还可以使用项目。

1. 登录到 Azure 门户中，选择**所有服务**，然后搜索 Azure Migrate。
2. 下**Services**，选择**Azure Migrate**。

   ![Azure Migrate-选择服务](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. 上**概述**页上，选择**评估和迁移数据库**。

   ![Azure Migrate-启动评估](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. 在中**数据库**下**入门**，选择**添加工具**。

   ![Azure Migrate-添加工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. 上**迁移项目**选项卡上，选择你的 Azure 订阅和资源组 （如果还没有资源组中，创建一个）。
6. 下**项目详细信息**，指定项目名称和要在其中创建该项目在地理位置。

    ![Azure Migrate-添加工具对话框](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    您可以在任何这些地理区域中创建 Azure Migrate 项目。

    | **地域**  | **存储位置区域** |
    | ------------- | ------------- |
    | 亚洲 | 亚洲东南部或亚洲东部 |
    | Europe | 欧洲北部或欧洲西部 |
    | United Kingdom | 英国南部或英国西部 |
    | United States | 美国中部或美国西部 2 |

    为项目指定地理位置仅用于存储从本地 Vm 中收集的元数据。 您可以选择在实际迁移任何目标区域。

7. 选择**下一步**，以及如何将评估工具。

   > [!NOTE]
   > 当你创建项目时，必须添加至少一个评估或迁移工具。

8. 上**选择评估工具**选项卡上， **Azure Migrate:数据库的评估**显示为评估工具，用于添加。 如果当前不需要评估工具，请选择**跳过现在添加评估工具**复选框。 选择“**下一步**”。

    ![Azure Migrate-选择评估工具的选项卡](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. 上**选择迁移工具**选项卡上， **Azure Migrate:数据库迁移**显示为迁移工具，用于添加。 如果当前不需要迁移工具，请选择**跳过添加迁移工具现在**。 选择“**下一步**”。

    ![Azure Migrate-选择迁移工具的选项卡](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. 在中**查看 + 添加工具**，查看设置，然后选择**将工具添加**。

    ![Azure Migrate-查看 + 添加工具选项卡](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    创建项目后，可以选择用于评估和迁移的服务器和工作负荷、 数据库和 web 应用的其他工具。

## <a name="assess-and-upload-assessment-results"></a>评估并上传评估结果

已成功在创建迁移项目之后,**评估工具**，请在**Azure Migrate:数据库的评估**框中，用于下载和使用数据迁移助手工具显示的说明。

   ![Azure Migrate-要添加的评估工具](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. 下载数据迁移助手使用提供的链接并安装有权访问源 SQL Server 实例的计算机上。
2. 启动数据迁移助手。

### <a name="create-an-assessment"></a>创建评估

1. 在左侧，选择 **+** 图标，并选择评估**项目类型**
2. 指定项目名称，并选择源服务器和目标服务器类型。

    如果您要升级的本地 SQL Server 实例到更高版本的 SQL Server 或 Azure VM 上托管的 SQL Server，源和目标服务器类型设置为**SQL Server**。 将目标服务器类型设置为**Azure SQL 数据库托管实例**为 Azure SQL 数据库 (PaaS) 目标准备情况评估。

3. 选择“创建”  。

   ![Azure Migrate-数据迁移助手界面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>选择评估选项

1. 选择报表类型。

    可以选择一个或两个以下报表类型：
    * 检查数据库兼容性
    * 检查功能奇偶一致性

   ![Azure Migrate-数据迁移助手-评估选项屏幕](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. 选择“**下一步**”。

### <a name="add-databases-to-assess"></a>添加要评估的数据库

1. 选择**添加源**打开连接飞出菜单。
2. 输入 SQL server 实例名称，选择身份验证类型、 设置正确的连接属性，并选择**Connect**。
3. 选择要评估和选择的数据库**添加**。

   > [!NOTE]
   > 可以通过选择时按住 Shift 或 Ctrl 键，并单击删除源中删除多个数据库。 你可以通过使用添加源按钮从多个 SQL Server 实例中添加数据库。

4. 选择**下一步**，开始评估。

   ![Azure Migrate-数据迁移助手-选择源屏幕](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 评估完成后，选择**将上传到 Azure Migrate**。

   ![Azure Migrate-数据迁移助手-查看结果屏幕](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. 登录 Azure 门户。

   ![Azure Migrate-数据迁移助手-查看结果屏幕](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 选择要在其中上传的评估结果，并选择订阅和 Azure Migrate 项目**上传**。

   等待评估上传确认。

## <a name="view-target-readiness-assessment-results"></a>查看目标准备情况评估结果

1. 登录 Azure 门户中，搜索 Azure migrate，然后选中**Azure Migrate**。

   ![Azure Migrate-Azure 门户-服务搜索](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. 选择**评估数据库迁移**获取到的评估结果。

   ![Azure Migrate-查看评估结果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    可以查看 SQL Server 准备情况摘要，请确保位于正确的迁移项目，否则，使用更改选项以选择一个不同的迁移项目。

    每次您更新的评估结果为 Azure 迁移项目，Azure 迁移中心整合所有结果并提供摘要报告。  可以并行执行多个数据迁移助手的评估，并将结果上传到单一迁移项目，以获得统一的准备情况报告。

   ![Azure 迁移的准备情况检查结果](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **评估数据库实例**:到目前为止评估 SQL Server 实例数。
    **评估数据库**:评估评估的一个或多个 SQL Server 实例之间的数据库总数**数据库可供 SQL DB**:准备好迁移到 Azure SQL 数据库 (PaaS) 数据库的数目。
    **数据库可供 Azure SQL VM**:数据库数量但准备迁移到 Azure SQL Server Vm 包含一个或多个迁移阻止程序到 Azure SQL 数据库 (PaaS)。

3. 选择**评估数据库实例**转到 SQL Server 实例级别视图。

   ![Azure Migrate-查看实例准备情况](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    您可以找到每个 SQL Server 实例迁移到 Azure SQL 数据库 (PaaS) 的百分比就绪状态。

4. 选择要转到的数据库准备情况视图的特定实例。

   ![Azure Migrate-查看数据库准备情况](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    您可以看到多个迁移阻止程序按每个数据库，每个上述视图中的每个数据库建议的目标。

5. 查看 DMA 评估结果，以获取更多详细信息迁移阻止程序。

   ![Azure Migrate-查看迁移阻止程序](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>请参阅

* [数据迁移助手 (DMA)](../dma/dma-overview.md)
* [数据迁移助手：配置设置](../dma/dma-configurationsettings.md)
* [数据迁移助手：最佳做法](../dma/dma-bestpractices.md)
