---
title: WideWorldImporters OLAP 数据库-使用 SQL Server |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 1e6155be9338f7d7c04c7ecfd5312d38d909065e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628133"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW 使用的 SQL Server 特性和功能
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 旨在展示许多适用于数据仓库和分析 SQL Server 的主要功能。 下面是 SQL Server 特性和功能，以及如何在 WideWorldImportersDW 中使用的说明的列表。

## <a name="polybase"></a>PolyBase

[适用于 SQL Server 2016 和更高版本]

使用 PolyBase 将 WideWorldImportersDW 来自销售信息组合使用人口统计信息来了解哪些城市可能感兴趣的销售额的更多扩展有关的公共数据集。

若要启用示例数据库中的使用 PolyBase，请确保已安装，并在数据库中运行以下存储的过程：

    EXEC [Application].[Configuration_ApplyPolybase]

这将创建外部表`dbo.CityPopulationStatistics`引用包含在美国，托管在 Azure blob 存储中的城市的人口数据的公共数据集。 建议以查看存储过程以了解配置过程中的代码的。 如果你想要托管在 Azure blob 存储中的数据和确保其安全从常规公共访问权限，你需要时需要执行其他配置步骤。 以下查询返回的数据从外部数据集：

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

若要了解哪些城市可能感兴趣的更多扩展，以下查询查看的城市，增长率，并返回前 100 个最大城市重要的业务增长，并且 Wide World Importers 没有销售业务。 查询涉及远程表之间的联接`dbo.CityPopulationStatistics`和本地表`Dimension.City`，并涉及本地表的筛选器`Fact.Sales`。

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>聚集列存储索引

（此示例的完整版本）

与所有事实表，使用聚集列存储索引 (CCI) 来减少存储占用并提高查询性能。 使用 CCI，事实表的基本存储使用列压缩。

除了聚集列存储索引中，使用非聚集索引来促进主键和外键约束。 超出了丰富的警告： 添加了这些约束-ETL 过程源具有约束强制实施完整性的 WideWorldImporters 数据库中的数据。 删除主键和外键约束和它们支持的索引将减少这一事实表的存储占用。

**数据大小**

示例数据库具有有限的数据的大小，以使其易于下载和安装该示例。 但是，若要查看列存储索引的实际性能优势，您可能需要使用更大的数据集。

可以运行以下语句以增加的大小`Fact.Sales`通过插入示例数据的另一个 12 万行的表。 这些所有插入行的 2012 年，只有使用 ETL 过程不会相互干扰。

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

此语句将需要大约 5 分钟运行。 若要插入超过 120 万行，请将传递所需的要作为此存储过程的参数插入的行数。

若要比较使用和不使用列存储的查询性能，您可以删除和/或重新创建聚集列存储索引。

若要删除的索引：

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

若要重新创建：

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>分区

（此示例的完整版本）

数据仓库中的数据大小会变得非常大。 因此它是使用分区管理的较大的表在数据库中存储的最佳做法。

更大的事实数据表的所有按年分区。 唯一的例外是`Fact.Stock Holdings`，这不是基于日期的并具有有限的数据大小与其他事实数据表进行比较。

用于所有已分区表的分区函数是`PF_Date`，并且正在使用分区方案为`PS_Date`。

## <a name="in-memory-oltp"></a>内存中 OLTP

（此示例的完整版本）

WideWorldImportersDW 为临时表使用 SCHEMA_ONLY 内存优化表。 所有`Integration.` * `_Staging`表是 SCHEMA_ONLY 内存优化表。

SCHEMA_ONLY 表的优点是它们将不会记录，并且不需要任何磁盘访问。 这提高了 ETL 进程的性能。 由于这些表将不会记录，其内容将丢失，如果故障。 但是，数据源是仍然可用，因此 ETL 过程可以只需重新启动在失败时。
