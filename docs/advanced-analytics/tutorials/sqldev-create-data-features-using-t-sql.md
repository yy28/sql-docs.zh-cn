---
title: "第 4 课： 创建数据功能使用 T-SQL |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 5b2f4c44-6192-40df-abf1-fc983844f1d0
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f77e853d87c82cd6f2bd2a64e387ea3286eccfc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-4-create-data-features-using-t-sql"></a>第 4 课： 创建使用 T-SQL 的数据功能

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

本步骤中将学习如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数通过原始数据创建功能。 然后从存储过程调用该函数，创建包含该功能值的表。

## <a name="about-feature-engineering"></a>有关功能工程部门

几轮数据探索后，已从数据收集了一些见解，现可以继续“特征工程”。 此过程从原始数据创建有意义的功能是中创建分析模型的关键步骤。

在此数据集，距离值基于报告的计数距离，并不一定表示地理距离或实际的行程距离。 因此，需要使用源 NYC Taxi 数据集中提供的坐标计算接客点和落客点之间的直接距离。 可通过使用自定义 [函数中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine formula [!INCLUDE[tsql](../../includes/tsql-md.md)] （半正矢公式）实现。

使用一个自定义 T-SQL 函数 _fnCalculateDistance_通过半正矢公式计算距离，并使用另一个自定义 T-SQL 函数 _fnEngineerFeatures_创建包含所有功能的表。

整个过程是，如下所示：

- 创建执行计算的 T-SQL 函数

- 调用将生成功能数据的函数

- 功能数据保存到表

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>计算使用 fnCalculateDistance 的行程距离

该函数_fnCalculateDistance_应已下载并注册[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为本教程的准备工作的一部分。 花点时间查看代码。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依次展开“可编程性”、“函数”及“标量值函数”。   

2. 右键单击“fnCalculateDistance”，然后选择“修改”，以在新查询窗口中打开 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。
  
    ```SQL
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END
    GO
    ```
  
    - 该函数为标量值函数，返回预定义类型的单个数据值。
  
    - 它将从行程接客位置和落客位置获取的纬度和经度值作为输入。 半正矢公式会将位置转换为弧度值，并使用这些值以英里计算这两个位置之间的直接距离。

## <a name="generate-the-features-using-fnengineerfeatures"></a>生成使用的功能_fnEngineerFeatures_

若要添加到的表中可以用于定型模型的计算的值，你将使用另一个函数， _fnEngineerFeatures_。 新的函数调用以前创建的 T-SQL 的函数， _fnCalculateDistance_，若要获取的直接提取和放置位置距离。 

1. 花时间检查自定义 T-SQL 函数 _fnEngineerFeatures_的代码，该函数应已作为本演练准备工作的一部分进行了创建。
  
    ```SQL
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + 此表值函数，它接受多个列作为输入，并输出具有多个功能列的表。

    + 此函数的目的是在生成模型中创建新的功能，以供使用。

2.  若要验证此函数可，使用它来计算这些行程其中按流量计费的距离已 0 但的提取和放置的位置不同的地理距离。
  
    ```SQL
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    可见，仪表报告的距离并不始终对应于地理距离。 这就是特征工程很重要的原因。 你可以使用这些改进的数据功能训练机器学习模型使用。

## <a name="next-lesson"></a>下一课

[第 5 课： 训练和保存模型使用 T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>上一课

[第 3 课： 浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)
