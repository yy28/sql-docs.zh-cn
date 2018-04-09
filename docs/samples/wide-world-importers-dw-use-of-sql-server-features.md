---
title: WideWorldImporters OLAP 数据库-使用 SQL Server |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 09f85464d0fdb4674691d8d17e8a50e1881b8b6d
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2018
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW 使用 SQL Server 功能和功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
WideWorldImportersDW 旨在展示许多适用于数据仓库和分析 SQL Server 的主要功能。 下面是 SQL Server 功能和功能，以及如何在 WideWorldImportersDW 中使用的说明的列表。

## <a name="polybase"></a>PolyBase

[适用于 （2016年及更高版本） 的 SQL Server]

PolyBase 用于将从 WideWorldImportersDW 的销售信息与有关人口统计信息以了解哪些城市可能感兴趣的销售的进一步扩展了公共数据集结合起来。

若要使示例数据库中的 PolyBase 使用，请确保已安装，并在数据库中运行以下存储的过程：

    EXEC [Application].[Configuration_ApplyPolybase]

这将创建外部表`dbo.CityPopulationStatistics`引用包含在美国，托管在 Azure blob 存储中的城市的填充数据的公共数据集。 建议查看存储过程以了解配置过程中的代码的。 如果你想要承载您自己的数据在 Azure blob 存储和保护从常规公共访问权限，你将需要进行其他配置步骤。 以下查询从该外部的数据集返回的数据：

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

若要了解哪些城市可能感兴趣进一步扩展，以下查询查看城市，增长率，并返回前 100 个最大城市显著增长，并且 Wide World Importers 没有销售是否存在。 查询涉及到远程表之间的联接`dbo.CityPopulationStatistics`和本地表`Dimension.City`，和筛选器涉及本地表`Fact.Sales`。

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

聚集列存储索引 (CCI) 用于所有事实数据表，以减少存储需求量和提高查询性能。 CCI 使用的事实数据表的基本存储使用列压缩。

非聚集索引基于聚集列存储索引，用于简化主键和外键约束。 这些约束添加超出需要注意的众多-ETL 过程源具有约束来强制实现完整性的 WideWorldImporters 数据库中的数据。 删除主键和外键约束和其支持的索引，将减少的事实数据表的存储占用空间。

**数据大小**

示例数据库具有有限的数据大小，以便可以方便地下载并安装示例。 但是，若要查看列存储索引的实际性能优势，你想要使用的更大的数据集。

你可以运行以下语句以增加的大小`Fact.Sales`的方法是插入的示例数据的另一个 12 万行的表。 这些所有插入行年 2012，使 ETL 过程不干扰。

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

此语句将需要大约 5 分钟运行。 若要插入 12 多万行，请将传递所需的要作为参数传递给此存储过程插入的行数。

若要比较使用和不使用列存储的查询性能，你可以删除和/或重新创建聚集列存储索引。

若要删除索引：

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

若要重新创建：

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>分区

（此示例的完整版本）

数据仓库中的数据大小会变得非常大。 因此，最好使用分区管理的数据库中的大型表存储是它。

更大的事实数据表的所有按年进行分区。 唯一的例外是`Fact.Stock Holdings`、 这不是基于日期的和具有有限的数据大小相比于其他事实数据表。

用于所有已分区表的分区函数是`PF_Date`，并且正在使用分区方案为`PS_Date`。

## <a name="in-memory-oltp"></a>内存中 OLTP

（此示例的完整版本）

WideWorldImportersDW SCHEMA_ONLY 内存优化表用于临时表。 所有`Integration.` * `_Staging`表是 SCHEMA_ONLY 内存优化表。

SCHEMA_ONLY 表的优点是它们不作记录，并且不需要任何磁盘访问。 这提高了 ETL 过程的性能。 由于这些表不作记录，其内容都将丢失故障时。 但是，数据源仍然可用，因此 ETL 过程可以只需重新启动如果发生故障。
