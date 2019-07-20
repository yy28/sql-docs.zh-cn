---
title: 第2课使用 R 和 T-sql 函数创建数据功能
description: 本教程介绍如何将计算添加到存储过程中, 以便在 R 机器学习模型中使用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7570c6769a780c5a6d98bdfc762092524bf5000c
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345930"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>第 2 课：使用 R 和 T-sql 创建数据功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

本步骤中将学习如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数通过原始数据创建功能。 然后从存储过程调用该函数，创建包含该功能值的表。

## <a name="about-feature-engineering"></a>关于功能设计

几轮数据探索后，已从数据收集了一些见解，现可以继续“特征工程”  。 从原始数据创建有意义的功能的这一过程是创建分析模型的关键步骤。

在此数据集中, 距离值基于报告的计量距离, 不一定表示地理距离或旅行的实际距离。 因此，需要使用源 NYC Taxi 数据集中提供的坐标计算接客点和落客点之间的直接距离。 可通过使用自定义 [函数中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine formula [!INCLUDE[tsql](../../includes/tsql-md.md)] （半正矢公式）实现。

使用一个自定义 T-SQL 函数 _fnCalculateDistance_通过半正矢公式计算距离，并使用另一个自定义 T-SQL 函数 _fnEngineerFeatures_创建包含所有功能的表。

总体过程如下所示:

- 创建执行计算的 T-sql 函数

- 调用函数以生成功能数据

- 将功能数据保存到表

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>使用 fnCalculateDistance 计算行程距离

函数_fnCalculateDistance_应已下载并向注册[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 作为本教程准备工作的一部分。 花点时间查看代码。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依次展开“可编程性”  、“函数”  及“标量值函数”  。   

2. 右键单击“fnCalculateDistance”  ，然后选择“修改”  ，以在新查询窗口中打开 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。
  
    ```sql
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

## <a name="generate-the-features-using-fnengineerfeatures"></a>使用_fnEngineerFeatures_生成功能

若要将计算值添加到可用于定型模型的表中, 请使用另一个函数_fnEngineerFeatures_。 新函数调用以前创建的 T-sql 函数_fnCalculateDistance_, 以获取拾取位置与下拉位置之间的直接距离。 

1. 花时间检查自定义 T-SQL 函数 _fnEngineerFeatures_的代码，该函数应已作为本演练准备工作的一部分进行了创建。
  
    ```sql
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

    + 此表值函数将多个列作为输入, 并输出具有多个特征列的表。

    + 此函数的目的是创建新功能, 以用于生成模型。

2.  若要验证此函数是否正常工作, 请使用它来计算在按流量计费的距离为0但拾取和下拉位置不同的行程的地理距离。
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    可见，仪表报告的距离并不始终对应于地理距离。 这就是特征工程很重要的原因。 您可以使用这些改进的数据功能通过 R 来训练机器学习模型。

## <a name="next-lesson"></a>下一课

[第 3 课：使用 T-sql 定型和保存模型](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>上一课

[第 1 课：使用 R 和存储过程浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)
