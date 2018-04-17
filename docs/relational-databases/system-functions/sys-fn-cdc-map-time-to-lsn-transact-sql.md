---
title: sys.fn_cdc_map_time_to_lsn (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95ee3e6306b47f74d0787bf62e4bfe3ecd5e07c6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回的日志序列号 (LSN) 值**start_lsn**中的列[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)指定的时间的系统表。 你可以使用此函数能系统地将 datetime 范围映射到所需的变更数据捕获枚举函数基于 LSN 的范围[cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)和[cdc.fn_cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)以返回在该范围内的数据更改。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>参数  
 < relational_operator > {比小于最大 | 比大小于或等于 | 最小大于 | 最小大于或等于}  
 用于标识在内的不同 LSN 值**cdc.lsn_time_mapping**带有关联的表**tran_end_time**满足关系相比*tracking_time*值。  
  
 *relational_operator*是**nvarchar (30)**。  
  
 *tracking_time*  
 要进行匹配的日期时间值。 *tracking_time*是**datetime**。  
  
## <a name="return-type"></a>返回类型  
 **binary(10)**  
  
## <a name="remarks"></a>注释  
 若要了解如何**sys.fn_cdc_map_time_lsn**可以用于将 datetime 范围映射到 LSN 范围，请考虑以下方案。 假定使用者希望每日提取更改数据。 也就是说，使用者只需要给定日午夜之前（包括午夜）的更改。 此时间范围的下限应为无限接近前一天午夜的时间点（但不包括前一天午夜）。 上限应为给定日的午夜（包括午夜）。 下面的示例演示如何函数**sys.fn_cdc_map_time_to_lsn**可以用于系统地将此基于时间的范围映射到返回所有变更数据捕获枚举函数所都需的基于 LSN 的范围在该范围内的更改。  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 关系运算符 '`smallest greater than`' 用于将更改限制为在前一天的午夜后发生的更改。 如果多个条目具有不同的 LSN 值共享**tran_end_time**值标识为在下限[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)表，该函数将返回确保的最小 LSN所有项目都均包含。 有关绑定的上限，关系运算符`largest less than or equal to`用于确保区域包括那些具有作为午夜的那一天中包含的所有条目其**tran_end_time**值。 如果多个条目具有不同的 LSN 值共享**tran_end_time**值标识为上限，该函数将返回所有条目都都包含的最大 LSN。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例使用`sys.fn_cdc_map_time_lsn`函数来确定是否有中的任何行[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)表与**tran_end_time**大于或等于午夜的值。 例如，可以用此查询来确定捕获进程是否已处理完截至前一天午夜提交的更改，以便接下来可以提取当天的更改数据。  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>另请参阅  
 [cdc.lsn_time_mapping &#40;Transact SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
