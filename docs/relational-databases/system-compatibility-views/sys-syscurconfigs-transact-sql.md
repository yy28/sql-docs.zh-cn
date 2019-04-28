---
title: sys.syscurconfigs (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3ef0f49229ab374a0ca9e2dce12d7fa6ea5f59bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62693836"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对每个当前配置选项而言都包含一项。 该视图同时还包含四项，用于说明配置结构。 **syscurconfigs**由用户进行查询时动态生成。 有关详细信息，请参阅[sys.sysconfigures &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**value**|**int**|用户可修改的变量值。 仅在执行 RECONFIGURE 后，由[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]使用。|  
|**config**|**smallint**|配置变量号。|  
|**comment**|**nvarchar(255)**|对配置选项的解释。|  
|**status**|**smallint**|表示选项状态的位图。 可能的值包括：<br /><br /> 0 = 静态。 重新启动服务器后，设置才会生效。<br /><br /> 1 = 动态。 执行 RECONFIGURE 语句后，变量才会生效。<br /><br /> 2 = 高级。 显示变量时，才**显示高级选项**设置。<br /><br /> 3 = 动态和高级。|  
  
## <a name="see-also"></a>请参阅  
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
