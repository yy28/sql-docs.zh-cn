---
title: WideWorldImporters 生成数据的 SQL 示例数据库 |Microsoft Docs
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37988941"
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 数据生成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 数据库的已发布的版本已从 2013 年 1 月 1 日，最多天生成数据库的数据。

当您使用这些示例数据库时，您可能想要包括最新示例数据。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的数据生成

若要生成为当前日期的示例数据：

1. 如果你尚未这样做，安装全新版本的 WideWorldImporters 数据库。 有关安装说明，请参阅[安装和配置](wide-world-importers-oltp-install-configure.md)。
2. 在数据库中执行以下语句：

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    此语句将添加到数据库，截至当前日期的示例销售和采购数据。 它按天显示数据生成的进度。 数据生成可能需要大约 10 分钟需要数据每年。 数据生成一个随机因素，由于有生成运行之间的数据的一些差异。

    若要增加或减少生成的每日的订单的数据量，更改参数的值为`@AverageNumberOfCustomerOrdersPerDay`。 使用参数`@SaturdayPercentageOfNormalWorkDay`和`@SundayPercentageOfNormalWorkDay`来确定周末日期的订单数量。

## <a name="import-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW 中生成的导入数据

若要导入 WideWorldImportersDW OLAP 数据库中为当前日期的示例数据：

1. 通过使用在上一部分中的步骤在 WideWorldImporters OLTP 数据库中执行数据生成逻辑。
2. 如果你尚未这样做，安装 WideWorldImportersDW 数据库的干净的版本。 有关安装说明，请参阅[安装和配置](wide-world-importers-oltp-install-configure.md)。
3. 通过在数据库中执行以下语句对 OLAP 数据库重设种子：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 运行*每日 ETL.ispac*要将数据导入 OLAP 数据库的 SQL Server Integration Services 包。 若要了解如何运行 ETL 作业，请参阅[WideWorldImporters ETL 工作流](wide-world-importers-perform-etl.md)。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>进行性能测试中 WideWorldImportersDW 生成数据

WideWorldImportersDW 可以随意增加数据大小进行性能测试。 例如，它可以增加要使用聚集列存储索引使用的数据大小。

面临的挑战之一是使下载大小不足够小，以下载轻松，但大足以说明 SQL Server 性能的功能。 例如，对于列存储索引的显著好处时可实现仅使用更大数量的行。 

可以使用`Application.Configuration_PopulateLargeSaleTable`的步骤来增大中的行数`Fact.Sale`表。 在 2012年日历年，以避免冲突与 2013 年 1 月 1 日开始的现有全球进口商数据中插入这些行。

### <a name="procedure-details"></a>过程的详细信息

#### <a name="name"></a>“属性”

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parameters

  `@EstimatedRowsFor2012` **bigint** （具有默认值为 12000000）

#### <a name="result"></a>结果

大约所需的数量的行插入到`Fact.Sale`2012 年份中的表。 该过程人为限制为 50,000 每日的行数。 可以更改此限制，但限制可帮助您避免意外 overinflations 的表。

该过程也适用聚集列存储索引，如果尚未已应用。
