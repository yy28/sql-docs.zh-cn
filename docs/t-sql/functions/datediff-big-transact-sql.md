---
title: "DATEDIFF_BIG (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 08f27953aac5fa36f1b38e243d8465f57458dafe
ms.contentlocale: zh-cn
ms.lasthandoff: 10/12/2017

---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

返回指定的计数 （有符号大整数） *datepart*之间指定跨越边界*startdate*和*enddate*。
  
有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>参数  
*datepart*  
是的一部分*startdate*和*enddate* ，指定删除线的边界的类型。 下表列出所有有效*datepart*自变量。 用户定义的变量等效项是无效的。
  
|*datepart*|缩写形式|  
|---|---|
|**年**|**yy、 yyyy**|  
|**季度**|**qq、 q**|  
|**月**|**mm、 m**|  
|**dayofyear**|**dy、 y**|  
|**一天**|**dd、 d**|  
|**周**|**wk、 ww**|  
|**小时**|**hh**|  
|**分钟**|**mi、 n**|  
|**第二个**|**ss、 s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**纳秒为**|**ns**|  
  
*startdate*  
是可被解析为一个表达式**时间**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是表达式、 列表达式、 用户定义变量或字符串文本。 *startdate*减去*enddate*。  
为避免不确定性，请使用四位数年份。 两位数年份的相关信息，请参阅[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
*结束日期*  
请参阅*startdate*。
  
## <a name="return-type"></a>返回类型  
 已签名   
        **bigint**  
  
## <a name="return-value"></a>返回值  
指定的开始日期和结束日期之间交叉返回计数 (有符号 bigint) 的指定日期部分边界。
-   每个*datepart*和其缩写返回相同的值。  
  
如果返回的值超出范围**bigint** (-9223372036854775808 到 9223372036854775807) 返回一个错误。 有关**毫秒**，之间的最大偏差*startdate*和*enddate*是 24 天，20 小时 31 分钟和 23.647 秒。 有关**第二个**，最大的区别是 68 年。
  
如果*startdate*和*enddate*都分配只有一个时间值与*datepart*不是时间*datepart*，则返回 0。
  
时区偏移量的组件*startdate*或*endate*不用于计算的返回值。
  
因为[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)精确到最的分钟数，仅当**smalldatetime**值用于*startdate*或*enddate*(秒）和毫秒始终设置为在返回值为 0。
  
如果仅时间值分配给日期数据类型的变量，则缺少的日期部分的值将设置为默认值： 1900年-01-01。 如果仅日期值分配给时间或日期数据类型的变量，缺少的时间部分的值将设置为默认值： 00:00:00。 如果任一*startdate*或*enddate*具有仅时间部分和其他仅日期部分、 缺少时间和日期部分设置为默认值。
  
如果*startdate*和*enddate*不同日期数据类型和一个具有更多的时间部分或比另秒的小数部分精度，缺少的其他部分将设置为 0。
  
## <a name="datepart-boundaries"></a>日期部分边界
以下语句具有相同*startdate*和同一*endate*。 这些日期是相邻的，在时间上相差 .0000001 秒。 之间的差异*startdate*和*endate*在每个语句中跨越一个日历或时间边界的其*datepart*。 每个语句都返回 1。 如果对于此示例使用了不同年份，如果这两个*startdate*和*endate*处于同一个日历周的返回值**周**将为 0。

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>注释  
可以在选择列表中，使用 DATEDIFF_BIG，其中，组 BY 和 ORDER BY 子句。
  
DATEDIFF_BIG 隐式强制转换为字符串文本**datetime2**类型。 这意味着，DATEDIFF_BIG 不支持格式 YDM 日期传递作为字符串时。 必须显式强制转换为字符串**datetime**或**smalldatetime**要使用的 YDM 格式类型。
  
指定 SET DATEFIRST 具有 DATEDIFF_BIG 没有影响。 DATEDIFF_BIG 始终使用星期日是一周的第一天，以确保该函数是确定性。
  
## <a name="examples"></a>示例  
下面的示例使用不同类型的表达式作为自变量为*startdate*和*enddate*参数。
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>为 startdate 和 enddate 指定列  
下例计算一个表的两列中的日期之间所跨越的日边界数。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
很多其他示例，请参阅中的密切相关的示例[DATEDIFF &#40;Transact SQL &#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact SQL &#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  

