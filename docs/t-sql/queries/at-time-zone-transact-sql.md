---
title: "在时区 (Transact SQL) |Microsoft 文档"
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0983cbd76b1ec3a71985537f098f8faf002b93e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="at-time-zone-transact-sql"></a>在时区 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  将转换*inputdate*到相应*datetimeoffset*目标时区中的值。 如果*inputdate*提供如果没有偏移量的信息，函数将应用的假设的时区偏移量*inputdate*目标时区中提供值。 如果*inputdate*作为提供*datetimeoffset*值，比**AT TIME ZONE**子句将其转换为目标时区，使用时区转换规则。  
  
 **在时区**实现依赖于要转换的 Windows 机制**datetime**跨时区的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>参数  
 *inputdate*  
 是可被解析为一个表达式**smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。  
  
 *时区*  
 目标时区的名称。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]依赖于在 Windows 注册表中存储的时区。 在以下注册表配置单元存储在计算机上安装的所有时区： **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time 区域**。 通过公开了已安装的时间区域列表[sys.time_zone_info &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md)视图。  
  
## <a name="return-types"></a>返回类型  
 返回的数据类型**datetimeoffset**  
  
## <a name="return-value"></a>返回值  
 **Datetimeoffset**目标时区中的值。  
  
## <a name="remarks"></a>注释  
 **在时区**应用特定规则，用于转换中的输入的值**smalldatetime**， **datetime**和**datetime2**分为的数据类型受影响的间隔由 DST 更改：  
  
-   本地时间的持续时间取决于时钟调整的持续时间中存在间隔则的时钟设置继续操作时 （通常为 1 小时，但它可以是 30 或 45 分钟，具体取决于时区）。 属于此间隙时间点的偏移量的转换在这种情况下，*后*DST 更改。  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- 当重新设置时钟时，然后 2 小时的本地时间重叠到一小时。  在这种情况下，属于重叠间隔时间点出现偏移量*之前*时钟更改：  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

由于某些信息 （如时区规则） 维护之外[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和随时会偶尔发生更改， **AT TIME ZONE**函数分类为具有不确定性。 
  
## <a name="examples"></a>示例  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. 将目标时区偏移量添加到不带偏移量的信息的日期时间  
 使用**AT TIME ZONE**添加偏移量基于时区规则，当你知道原始**datetime**相同的时区中提供值：  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. 不同时区之间转换值  
 下面的示例将转换不同时区之间的值：  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. 查询使用本地时区的临时表  
 下面的示例从临时表中选择数据。  
  
```  
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间类型](../../t-sql/data-types/date-and-time-types.md)   
 [日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  

