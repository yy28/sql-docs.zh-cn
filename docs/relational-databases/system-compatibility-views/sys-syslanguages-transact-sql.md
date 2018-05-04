---
title: sys.syslanguages (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.syslanguages
- sys.syslanguages_TSQL
- syslanguages
- syslanguages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syslanguages system table
- sys.syslanguages compatibility view
ms.assetid: f216d1cd-997c-42f0-a737-abbdfcd88383
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8de7878b5b718f5ebea26aea965b691d2bab5723
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="syssyslanguages-transact-sql"></a>sys.syslanguages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的每种语言都包含一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|langid|**int**|唯一语言 ID。|  
|dateformat|**nchar(3)**|日期顺序，如 DMY。|  
|datefirst|**tinyint**|每周的第一天：1 代表星期一，2 代表星期二，依此类推，直到 7 代表星期日。|  
|升级|**int**|预留给系统使用。|  
|name|**sysname**|正式语言名称，例如，Français。|  
|alias|**sysname**|代替语言名称，如 French。|  
|months|**nvarchar(372)**|以逗号分隔的月份名全称列表，按一月到十二月的顺序排列，每个名称最多可有 20 个字符。|  
|shortmonths|**nvarchar(132)**|以逗号分隔的月份名简称列表，按一月到十二月的顺序排列，每个名称最多可有 9 个字符。|  
|days|**nvarchar(217)**|以逗号分隔的星期名称，按星期一到星期日的顺序排列，每个名称最多可有 30 个字符。|  
|lcid|**int**|语言的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 区域设置 ID。|  
|msglangid|**int**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]消息组 ID。|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]包含下列已安装的语言。  
  
|用英语表示的名称|Windows LCID|[!INCLUDE[ssDE](../../includes/ssde-md.md)]消息组 ID|  
|---------------------|------------------|-----------------------------------------|  
|英语|2052|2052|  
|德语|1031|1031|  
|法语|1036|1036|  
|日语|1041|1041|  
|丹麦语|1030|1030|  
|西班牙语|3082|3082|  
|意大利语|1040|1040|  
|荷兰语|1043|1043|  
|挪威语|2068|2068|  
|葡萄牙语|2070|2070|  
|芬兰语|1035|1035|  
|瑞典语|1053|1053|  
|捷克语|1029|1029|  
|匈牙利语|1038|1038|  
|波兰语|1045|1045|  
|罗马尼亚语|1048|1048|  
|克罗地亚语|1050|1050|  
|斯洛伐克语|1051|1051|  
|Slovene|1060|1060|  
|希腊语|1032|1032|  
|保加利亚语|1026|1026|  
|俄语|1049|1049|  
|土耳其语|1055|1055|  
|英国英语|2057|2052|  
|爱沙尼亚语|1061|1061|  
|拉脱维亚语|1062|1062|  
|立陶宛语|1063|1063|  
|葡萄牙语（巴西）|1046|1046|  
|繁体中文|1028|1028|  
|朝鲜语|1042|1042|  
|简体中文|2052|2052|  
|阿拉伯语|1025|1025|  
|泰国语|1054|1054|  
  
## <a name="see-also"></a>另请参阅  
 [兼容性视图&#40;Transact SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [将系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
