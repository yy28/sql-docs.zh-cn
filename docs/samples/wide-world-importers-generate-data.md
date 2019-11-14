---
title: 在 SQL 示例中生成数据 WideWorldImporters
ms.date: 04/04/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0f880ea881b53c2600fb1fffdf7da5d16ab8d423
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056284"
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 数据生成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 数据库的已发布版本具有从2013年1月1日到数据库生成日期的数据。

使用这些示例数据库时，可能需要包含更多最新的示例数据。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的数据生成

若要生成最新日期的示例数据，请执行以下操作：

1. 如果尚未安装，请安装干净版本的 WideWorldImporters 数据库。 有关安装说明，请参阅[安装和配置](wide-world-importers-oltp-install-configure.md)。
2. 在数据库中执行以下语句：

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    此语句将示例销售和采购数据添加到数据库中，直到达到当前日期。 它按天显示数据生成的进度。 每年需要数据的数据生成可能需要大约10分钟。 由于数据生成的随机因素，在运行之间生成的数据存在一些差异。

    若要增加或减少每天生成的订单数，请更改参数 `@AverageNumberOfCustomerOrdersPerDay`的值。 使用参数 `@SaturdayPercentageOfNormalWorkDay` 和 `@SundayPercentageOfNormalWorkDay` 确定周末的订单量。

## <a name="import-generated-data-in-wideworldimportersdw"></a>导入在 WideWorldImportersDW 中生成的数据

若要将示例数据导入到 WideWorldImportersDW OLAP 数据库中的当前日期：

1. 使用上一节中的步骤执行 WideWorldImporters OLTP 数据库中的数据生成逻辑。
2. 如果尚未这样做，请安装 WideWorldImportersDW 数据库的干净版本。 有关安装说明，请参阅[安装和配置](wide-world-importers-oltp-install-configure.md)。
3. 通过在数据库中执行以下语句来重新设定 OLAP 数据库的种子：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 运行*每日 .ispac* SQL Server Integration Services 包，将数据导入到 OLAP 数据库。 若要了解如何运行 ETL 作业，请参阅[WIDEWORLDIMPORTERS ETL 工作流](wide-world-importers-perform-etl.md)。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>在 WideWorldImportersDW 中生成数据以执行性能测试

WideWorldImportersDW 可以任意增加用于性能测试的数据大小。 例如，它可以增加用于聚集列存储索引的数据大小。

其中一项难题是将下载内容的大小保持在足够小，以方便地下载，但足以演示 SQL Server 性能功能。 例如，仅当使用较大的行时，才会实现列存储索引的重要优势。 

您可以使用 `Application.Configuration_PopulateLargeSaleTable` 过程来增加 `Fact.Sale` 表中的行数。 行将在2012日历年中插入，以避免与开始2013年1月1日起的现有世界范围导入程序数据发生冲突。

### <a name="procedure-details"></a>过程详细信息

#### <a name="name"></a>NAME

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>参数

  `@EstimatedRowsFor2012` **bigint** （默认值为12000000）

#### <a name="result"></a>结果

在2012年中，大约将所需的行数插入到 `Fact.Sale` 表中。 过程人为每天将行数限制为50000。 您可以更改此限制，但该限制有助于避免意外的表 overinflations。

此过程还会应用聚集列存储索引（如果尚未应用）。
