---
title: Python + T-SQL：数据特征
description: 本教程介绍如何将计算添加到存储过程中，以便在 Python 机器学习模型中使用。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98a1ca3b012c5580e55dd6ea963c3869269f7136
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775342"
---
# <a name="create-data-features-using-t-sql"></a>使用 T-SQL 创建数据特征
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

进行数据探索后，已从数据中收集了一些见解，现在可以继续执行*特征工程*任务。 根据原始数据创建特征的过程可能是高级分析建模中的关键步骤。

本文属于[适用于 SQL 开发者的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)这一教程。 

本步骤中将学习如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数通过原始数据创建功能。 然后从存储过程调用该函数，创建包含该功能值的表。

## <a name="define-the-function"></a>定义函数

原始数据中报告的距离值是基于所报告的计量距离得出的，并不一定表示地理距离或行程距离。 因此，需要使用源 NYC Taxi 数据集中提供的坐标计算接客点和落客点之间的直接距离。 可通过使用自定义 [函数中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine formula [!INCLUDE[tsql](../../includes/tsql-md.md)] （半正矢公式）实现。

使用一个自定义 T-SQL 函数 _fnCalculateDistance_通过半正矢公式计算距离，并使用另一个自定义 T-SQL 函数 _fnEngineerFeatures_创建包含所有功能的表。

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>使用 fnCalculateDistance 计算行程距离

1.  应已下载 _fnCalculateDistance_ 函数，并作为本演练准备工作的一部分向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 注册。 花点时间查看代码。
  
    在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依次展开“可编程性”  、“函数”  及“标量值函数”  。
    右键单击“fnCalculateDistance”  ，然后选择“修改”  ，以在新查询窗口中打开 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function that calculates the direct distance between two geographical coordinates
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
注意： 

- 该函数为标量值函数，返回预定义类型的单个数据值。
- 它将从行程接客位置和落客位置获取的纬度和经度值作为输入。 半正矢公式会将位置转换为弧度值，并使用这些值以英里计算这两个位置之间的直接距离。

要将计算所得值添加到可用于定型模型的表，需使用另一个函数 _fnEngineerFeatures_。

### <a name="save-the-features-using-_fnengineerfeatures_"></a>使用 _fnEngineerFeatures_ 保存特征

1.  花时间检查自定义 T-SQL 函数 _fnEngineerFeatures_的代码，该函数应已作为本演练准备工作的一部分进行了创建。
  
    此函数为表值函数，将多个列作为输入，输出一个具有多个功能列的表。  此函数的目的是创建一个用于构建模型的功能集。 _fnEngineerFeatures_ 函数调用之前创建的 T-SQL 函数 _fnCalculateDistance_，以获得接客位置和落客位置之间的直接距离。
  
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
  
2. 要验证此函数是否正常运行，可用其计算一些计量距离为 0、但接客位置和落客位置不同的行程的地理距离。
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    可见，仪表报告的距离并不始终对应于地理距离。 这就是特征工程很重要的原因。

下一步将了解如何使用这些数据特征来创建和定型使用 Python 的机器学习模型。

## <a name="next-step"></a>后续步骤

[使用 T-SQL 定型和保存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一步

[浏览并可视化数据](sqldev-py3-explore-and-visualize-the-data.md)


