---
title: dbo.sysschedules (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs:
- TSQL
helpviewer_keywords:
- sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a1922fd8b9cdfb327186afe453fc1904d698579
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470709"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业计划的信息。 此表存储中**msdb**数据库。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业计划 ID。|  
|**schedule_uid**|**uniqueidentifier**|作业计划的唯一标识符。 此值用于标识分布式作业的计划。|  
|**originating_server_id**|**int**|作为作业计划来源的主服务器 ID。|  
|**名称**|**sysname (nvarchar(128))**|作业计划的用户定义名称。 该名称在作业中必须唯一。|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *security_identifier*的用户或组拥有的作业计划。|  
|**enabled**|**int**|作业计划的状态：<br /><br /> **0** = 未启用。<br /><br /> **1** = 启用。<br /><br /> 如果未启用计划，则不会运行该计划中的任何作业。|  
|**freq_type**|**int**|此计划中作业运行的频率。<br /><br /> **1** = 仅一次<br /><br /> **4** = 每日<br /><br /> **8** = 每周<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相对于**freq_interval**<br /><br /> **64** = SQL Server 代理服务启动时运行<br /><br /> **128** = 在计算机处于空闲状态时运行|  
|**freq_interval**|**int**|执行作业的间隔天数。 上的值取决于**freq_type**。 默认值是**0**，这指示**freq_interval**是未使用。 请参阅下表中的可能的值和其效果。|  
|**freq_subday_type**|**int**|单位**freq_subday_interval**。 以下是可能的值和及其说明。<br /><br /> <br /><br /> **1** :在指定的时间<br /><br /> **2** :Seconds<br /><br /> **4** :Minutes<br /><br /> **8** :Hours|  
|**freq_subday_interval**|**int**|数**freq_subday_type**周期每次执行作业之间。|  
|**freq_relative_interval**|**int**|当**freq_interval**如果在每个月内，会发生**freq_interval**是**32** （每月相对）。 可以是以下值之一：<br /><br /> **0** = **freq_relative_interval**是未使用<br /><br /> **1** = 第一次<br /><br /> **2** = 第二个<br /><br /> **4** = 第三次<br /><br /> **8** = 第四次<br /><br /> **16** = 最后一次|  
|**freq_recurrence_**<br /><br /> **factor**|**int**|在计划的作业执行之间间隔的周数或月数。 **freq_recurrence_factor**时才使用**freq_type**是**8**， **16**，或**32**。 如果此列包含**0**， **freq_recurrence_factor**是未使用。|  
|**active_start_date**|**int**|可以开始执行作业的日期。 日期的格式为 YYYYMMDD。 NULL 表示当天的日期。|  
|**active_end_date**|**int**|可以停止执行作业的日期。 日期格式为 YYYYMMDD。|  
|**active_start_time**|**int**|之间的任何日期时间**active_start_date**并**active_end_date**开始执行该作业。 时间格式为 HHMMSS，采用 24 小时制。|  
|**active_end_time**|**int**|之间的任何日期时间**active_start_date**并**active_end_date**停止执行该作业。 时间格式为 HHMMSS，采用 24 小时制。|  
|**date_created**|**datetime**|创建计划的日期和时间。|  
|**date_modified**|**datetime**|上次修改计划的日期和时间。|  
|**version_number**|**int**|计划的当前版本号。 例如，如果计划已修改 10 次**version_number**为 10。|  
  
|freq_type 的值|对 freq_interval 的影响|  
|-------------------------|------------------------------|  
|**1** （一次）|**freq_interval**未使用 (**0**)|  
|**4** （每日）|每个**freq_interval**天|  
|**8** （每周）|**freq_interval**是一个或多项操作：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **4** = 星期二<br /><br /> **8** = 星期三<br /><br /> **16** = 星期四<br /><br /> **32** = 星期五<br /><br /> **64** = 星期六|  
|**16** （每月）|上**freq_interval**月份中的天|  
|**32** （每月，相对）|**freq_interval**是以下之一：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 天<br /><br /> **9** = 工作日<br /><br /> **10** = 休息日|  
|**64** （SQL Server 代理服务启动时启动）|**freq_interval**未使用 (**0**)|  
|**128** （运行时计算机处于空闲状态）|**freq_interval**未使用 (**0**)|  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysjobschedules &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
