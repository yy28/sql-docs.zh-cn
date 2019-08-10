---
title: 执行 SQL Server 迁移评估 (数据迁移助手) |Microsoft Docs
description: 了解如何在迁移到另一个 SQL Server 或 Azure SQL 数据库之前, 使用数据迁移助手评估本地 SQL Server
ms.custom: ''
ms.date: 08/08/2019
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
ms.openlocfilehash: e14fc009944f28adb793ef3f89bb93f716a9ac58
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892686"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>使用数据迁移助手执行 SQL Server 迁移评估

下面的分步说明可帮助你通过使用数据迁移助手执行迁移到本地 SQL Server、SQL Server 在 Azure VM 或 Azure SQL 数据库上运行的第一个评估。

## <a name="create-an-assessment"></a>创建评估

1. 选择 "**新建**(+)" 图标, 然后选择 "**评估**" 项目类型。

2. 设置源和目标服务器类型。

    如果要将本地 SQL Server 实例升级到现代的本地 SQL Server 实例或托管在 Azure VM 上的 SQL Server, 请将源和目标服务器类型设置为 " **SQL Server**"。 如果要迁移到 Azure SQL 数据库, 请改为将目标服务器类型设置为 " **AZURE Sql 数据库**"。

3. 单击 **“创建”** 。

   ![创建评估](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>选择评估选项

1. 选择要迁移到的目标 SQL Server 版本。

2. 选择 "报表类型"。

   评估源 SQL Server 实例以迁移到本地 SQL Server SQL Server 或托管在 Azure VM 目标上时, 可以选择以下一种或两种评估报表类型:

    - **兼容性问题**
    - **新功能的建议**

   ![为 SQL Server 目标选择评估报告类型](../dma/media/dma-assesssqlonprem/assessment-types.png)

   评估源 SQL Server 实例以迁移到 Azure SQL 数据库时, 可以选择以下一种或两种评估报表类型:

    - **检查数据库兼容性**
    - **检查功能奇偶校验**

    ![选择 SQL 数据库目标的评估报表类型](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>添加数据库和扩展事件跟踪以进行评估

1. 选择 "**添加源**" 以打开 "连接" 弹出菜单。

2. 输入 SQL server 实例名称, 选择 "身份验证类型", 设置正确的连接属性, 然后选择 "**连接**"。

3. 选择要评估的数据库, 然后选择 "**添加**"。

    > [!NOTE]
    > 可以通过在按住 Shift 或 Ctrl 键的同时选择多个数据库, 然后单击 "**删除源**" 来删除多个数据库。 还可以通过选择 "**添加源**", 从多个 SQL Server 实例添加数据库。

4. 如果有任何即席或动态 SQL 查询或通过应用程序数据层启动的任何 DML 语句, 请输入文件夹的路径, 在该文件夹中, 将收集的所有扩展事件会话文件放在源上, 以捕获工作负荷 SQL Server.

     下面的示例演示如何在源 SQL Server 上创建扩展事件会话, 以捕获应用程序数据层工作负载。  捕获表示高峰工作负荷的持续时间的工作负荷。

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_statement_completed( 
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

5. 单击 "**下一步**" 开始评估。

    ![添加源并开始评估](../dma/media/dma-assesssqlonprem/select-database1.png)

## <a name="view-results"></a>查看结果

评估的持续时间取决于添加的数据库数和每个数据库的架构大小。 为每个数据库提供结果后, 就会显示结果。

1. 选择已完成评估的数据库, 然后使用切换器在**兼容性问题**和**功能建议**之间切换。

2. 查看在 "**选项**" 页上选择的目标 SQL Server 版本所支持的所有兼容性问题。

您可以通过分析受影响的对象及其详细信息来查看兼容性问题, 并可能针对在中断性**更改**、**行为更改**和已**弃用的功能**下标识的每个问题提供修补程序。

![查看评估结果](../dma/media/dma-assesssqlonprem/review-results.png)

同样, 你可以跨**性能**、**存储**和**安全**区域查看功能建议。

功能建议涵盖了不同类型的功能, 例如内存中 OLTP、列存储、Stretch Database、Always Encrypted、动态数据掩码和透明数据加密。

![查看功能建议](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

对于 Azure SQL 数据库, 评估提供了迁移阻止问题和功能奇偶校验问题。 通过选择特定的选项来查看这两种类别的结果。

- **SQL Server 功能奇偶校验**类别提供了一套全面的建议、Azure 中可用的替代方法和缓解措施。 它可帮助你在迁移项目中规划此项工作。

  ![查看 SQL Server 功能奇偶校验的信息](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- **兼容性问题**类别提供部分支持或不支持的功能, 这些功能会阻止本地 SQL Server 数据库迁移到 Azure SQL 数据库。 然后, 它提供了帮助你解决这些问题的建议。

  ![查看兼容性问题](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>针对目标准备情况评估数据场所

如果要进一步将这些评估扩展到整个数据空间, 并查找 SQL Server 实例和数据库迁移到 Azure SQL 数据库的相对就绪性, 请选择 "**上载到**" 以将结果上传到 azure 迁移中心 Azure Migrate.

这样, 便可以在 Azure 迁移中心项目上查看合并的结果。

[此处](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)提供了有关目标准备情况评估的详细的分步指南。

   ![将结果上传到 Azure Migrate](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>导出结果

在所有数据库都完成评估后, 选择 "**导出报告**" 将结果导出到 JSON 文件或 CSV 文件。 然后, 您就可以方便地分析数据。

你可以同时运行多个评估, 并打开 "**所有评估**" 页查看评估状态。
