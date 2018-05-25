---
title: WideWorldImporters 生成数据的 SQL 示例数据库 |Microsoft 文档
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ace1f771ef3a77a6f7db0072442affe181d7872
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 数据生成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 数据库的已发布的版本具有从 2013 年 1 月 1 日，最多天生成数据库的数据。

当你使用这些示例数据库时，你可能想要包括最新示例数据。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的数据生成

若要生成截至当前日期的示例数据：

1. 如果你尚未这样做，则安装 WideWorldImporters 数据库的清洁版本。 有关安装说明，请参阅[安装和配置](wide-world-importers-oltp-install-configure.md)。
2. 在数据库中执行以下语句：

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    此语句将添加到数据库，截至当前日期的示例销售和采购数据。 它按天显示的数据生成的进度。 数据生成可能需要大约 10 分钟时间供需要数据每年。 由于在数据生成一个随机因子，有一些差异的生成运行之间的数据。

    若要增加或减少生成的每日的订单的数据量，请更改参数的值`@AverageNumberOfCustomerOrdersPerDay`。 使用参数`@SaturdayPercentageOfNormalWorkDay`和`@SundayPercentageOfNormalWorkDay`以确定周末天订单量。

## <a name="import-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW 中生成的导入数据

导入到 WideWorldImportersDW OLAP 数据库中的当前日期的示例数据：

1. 通过使用上一节中的步骤执行 WideWorldImporters OLTP 数据库中的数据生成逻辑。
2. 如果你尚未尚未这样做，则安装 WideWorldImportersDW 数据库的清洁版本。 有关安装说明，请参阅[安装和配置](wide-world-importers-oltp-install-configure.md)。
3. 种子 OLAP 数据库重新设定通过数据库中执行以下语句：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 运行*每日 ETL.ispac*要将数据导入 OLAP 数据库的 SQL Server Integration Services 包。 若要了解如何运行 ETL 作业，请参阅[WideWorldImporters ETL 工作流](wide-world-importers-perform-etl.md)。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>在 WideWorldImportersDW 中生成数据，进行性能测试

WideWorldImportersDW 任意可以增加进行性能测试的数据大小。 例如，就有可能增加要使用聚集列存储索引使用的数据大小。

面临的挑战之一是保持下载的大小足够小，无法下载轻松，但大型足以演示 SQL Server 性能功能。 例如，仅当您使用更大数量的行时，可以获得显著的好处的列存储索引。 

你可以使用`Application.Configuration_PopulateLargeSaleTable`的步骤来增大中的行数`Fact.Sale`表。 在 2012年日历年，以避免与现有开始 2013 年 1 月 1 日的 World Wide Importers 数据冲突中插入行。

### <a name="procedure-details"></a>过程的详细信息

#### <a name="name"></a>名称

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parameters

  `@EstimatedRowsFor2012` **bigint** （与默认值为 12000000）

#### <a name="result"></a>结果

大约所需的行数插入到`Fact.Sale`2012 年中的表。 该过程人为地限制为 50000 每日的行数。 你可以更改此限制，但限制可帮助你避免意外 overinflations 的表。

该过程也适用聚集列存储索引如果它尚未已应用。
