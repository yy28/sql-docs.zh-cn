---
title: WideWorldImporters 生成数据的 SQL 示例数据库 |Microsoft 文档
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- " database-engine "
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: d99cdfacbe08cd3b81fb46bb61b49cab290780f4
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 数据生成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 数据库的已发布的版本包含数据开始 2013 年 1 月 1，最多天生成这些数据库。

如果使用了示例数据库，可能有益包括最新示例数据。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的数据生成

若要生成截至当前日期的示例数据，请按照下列步骤：

1. 如果尚未这样做，安装 WideWorldImporters 数据库的干净的版本。 有关安装说明， **WideWorldImporters 安装和配置**。
2. 在数据库中执行以下语句：

```
    EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
        @AverageNumberOfCustomerOrdersPerDay = 60,
        @SaturdayPercentageOfNormalWorkDay = 50,
        @SundayPercentageOfNormalWorkDay = 0,
        @IsSilentMode = 1,
        @AreDatesPrinted = 1;
```

此语句将添加在数据库中，截至当前日期的示例销售和采购数据。 它生成日常输出数据的进度。 可能需要大约 10 分钟时间供需要数据每年。 有一些差异的运行，因为有处于数据生成一个随机因子之间生成的数据。

若要增加或减少的生成，在每日的订单方面的数据量更改参数的值`@AverageNumberOfCustomerOrdersPerDay`。 参数`@SaturdayPercentageOfNormalWorkDay`和`@SundayPercentageOfNormalWorkDay`用于确定周末天订单量。

## <a name="importing-generated-data-in-wideworldimportersdw"></a>导入 WideWorldImportersDW 中生成的数据

要导入 OLAP 数据库 WideWorldImportersDW 中的当前日期之前的示例数据，请按照下列步骤：

1. 在 WideWorldImporters OLTP 数据库中，使用上述步骤中执行数据生成逻辑。
2. 如果尚未这样做，则安装 WideWorldImportersDW 数据库的清洁版本。 有关安装说明， **WideWorldImporters 安装和配置**。
3. 种子 OLAP 数据库重新设定通过数据库中执行以下语句：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 运行 SSIS 包**每日 ETL.ispac**若要将数据导入 OLAP 数据库。 有关如何运行 ETL 作业的说明，请参阅**WideWorldImporters ETL 工作流**。

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>性能测试中 WideWorldImportersDW 生成数据

WideWorldImportersDW 具有任意增加数据大小，为了性能测试，例如与聚集列存储功能。

面临的挑战之一是保持下载的大小足够小，无法下载轻松，但大型足以演示 SQL Server 性能功能。 例如，仅当使用更大数量的行时，会发生显著的好处的列存储索引。 

该过程`Application.Configuration_PopulateLargeSaleTable`可用来大幅提高中的行数`Fact.Sale`表。 请注意，在 2012年日历年，以避免与现有 World Wide Importers 数据开始在 2013 年 1 月 1 冲突中插入行。

### <a name="procedure-details"></a>过程的详细信息

#### <a name="name"></a>名称： 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>参数：

  `@EstimatedRowsFor2012` **bigint** （与默认值为 12000000）

#### <a name="result"></a>结果：

大约所需的行数插入到`Fact.Sale`2012 年中的表。 该过程人为地限制为 50000 每天的行数。 此限制可能会更改，但存在是为了避免意外 overinflations 的表。

此外，过程所适用聚集列存储索引，如果未已应用。
