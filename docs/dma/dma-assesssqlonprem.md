---
title: 执行 SQL Server 迁移评估
titleSuffix: Data Migration Assistant
description: 了解如何在迁移到其他 SQL 服务器或 Azure SQL 数据库之前使用数据迁移助手评估本地 SQL 服务器
ms.date: 01/15/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 59dc8c96ebda5ac66fb6701d480cb6d633e83158
ms.sourcegitcommit: 48e259549f65f0433031ed6087dbd5d9c0a51398
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "80809752"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>使用数据迁移助手进行 SQL Server 迁移评估

以下分步说明可帮助您使用数据迁移助手执行第一次评估，以便迁移到本地 SQL 服务器、在 Azure VM 上运行的 SQL Server 或 Azure SQL 数据库。

   > [!NOTE]
   > 数据迁移助手 v5.0 引入了对分析应用程序代码中的数据库连接和嵌入式 SQL 查询的支持。 有关详细信息，请参阅[博客文章"使用数据迁移助手评估应用程序的数据访问层](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)"。

## <a name="create-an-assessment"></a>创建评估

1. 选择 **"新建**（+）"图标，然后选择 **"评估**项目类型"。

2. 设置源和目标服务器类型。

    如果要将本地 SQL Server 实例升级到现代本地 SQL Server 实例或托管在 Azure VM 上的 SQL Server，请将源服务器和目标服务器类型设置为**SQL Server**。 如果要迁移到 Azure SQL 数据库，则改为将目标服务器类型设置为**Azure SQL 数据库**。

3. 单击“创建”。 

   ![创建评估](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>选择评估选项

1. 选择计划迁移到的目标 SQL Server 版本。

2. 选择报表类型。

   在评估源 SQL Server 实例以迁移到本地 SQL Server 或 Azure VM 目标上托管的 SQL Server 时，可以选择以下一种或两种评估报告类型：

    - **兼容性问题**
    - **新功能的建议**

   ![为 SQL Server 目标选择评估报告类型](../dma/media/dma-assesssqlonprem/assessment-types.png)

   在评估源 SQL Server 实例以迁移到 Azure SQL 数据库时，可以选择以下一种或两种评估报告类型：

    - **检查数据库兼容性**
    - **检查功能奇偶校验**

    ![为 SQL 数据库目标选择评估报告类型](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>添加数据库和扩展事件跟踪以评估

1. 选择 **"添加源**"以打开连接弹出窗口菜单。

2. 输入 SQL 服务器实例名称，选择身份验证类型，设置正确的连接属性，然后选择 **"连接**"。

3. 选择要评估的数据库，然后选择 **"添加**"。

    > [!NOTE]
    > 您可以通过在按住 Shift 或 Ctrl 键时选择多个数据库，然后单击"**删除源**"来删除多个数据库。 还可以通过选择 **"添加源**"从多个 SQL Server 实例添加数据库。

4. 如果您有任何临时或动态 SQL 查询或通过应用程序数据层启动的任何 DML 语句，请输入文件夹的路径，其中放置您收集的所有扩展事件会话文件以捕获源 SQL Server 上的工作负载。

     下面的示例演示如何在源 SQL Server 上创建扩展事件会话以捕获应用程序数据层工作负载。  捕获表示峰值工作负载的工期工作负载。

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. 单击“下一步”****，以开始评估。

    ![添加源并开始评估](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> 可以并发运行多个评估，然后打开“所有评估”页来查看评估的状态。****

## <a name="view-results"></a>查看结果

评估的持续时间取决于添加的数据库数和每个数据库的架构大小。 每个数据库的结果一旦可用，就会显示出来。

1. 选择已完成评估的数据库，然后使用切换器在**兼容性问题和****功能建议**之间切换。

2. 查看您在 **"选项**"页上选择的目标 SQL Server 版本支持的所有兼容性级别的兼容性问题。

您可以通过分析受影响的对象、其详细信息，以及针对 **"中断更改**、**行为更改**"和 **"弃用功能**"下标识的每个问题进行修复来查看兼容性问题。

![查看评估结果](../dma/media/dma-assesssqlonprem/review-results.png)

同样，您可以跨**性能**、**存储****和安全**区域查看功能建议。

功能建议涵盖不同类型的功能，如内存中 OLTP、列存储、拉伸数据库、始终加密、动态数据屏蔽和透明数据加密。

![查看功能建议](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

对于 Azure SQL 数据库，评估提供迁移阻止问题和功能奇偶校验问题。通过选择特定选项查看两个类别的结果。

- **SQL Server 功能奇偶校验**类别提供了一组全面的建议、Azure 中可用的替代方法以及缓解步骤。 它可以帮助您在迁移项目中规划此工作。

  ![查看 SQL Server 功能奇偶校验的信息](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- **兼容性问题**类别提供了部分支持或不支持的功能，这些功能阻止将本地 SQL Server 数据库迁移到 Azure SQL 数据库。然后，它提供建议以帮助您解决这些问题。

  ![查看兼容性问题](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>评估目标就绪性的数据区

如果希望进一步将这些评估扩展到整个数据区，并查找 SQL Server 实例和数据库的相对就绪性，以便迁移到 Azure SQL 数据库，请通过选择 **"上载到 Azure 迁移**"将结果上载到 Azure 迁移中心。

这样做允许您在 Azure 迁移中心项目上查看合并结果。

[此处](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)提供了目标就绪性评估的详细、分步指南。

   ![将结果上载到 Azure 迁移](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>导出结果

完成所有数据库评估后，选择 **"导出报告**"将结果导出到 JSON 文件或 CSV 文件。 然后，您可以自行分析数据。

## <a name="save-and-load-assessments"></a>保存和加载评估

除了导出评估结果外，还可以将评估详细信息保存到文件中并加载评估文件以供以后审阅。  有关详细信息，请参阅[文章"使用数据迁移助手保存和加载评估](../dma/dma-save-load-assessments.md)"。
