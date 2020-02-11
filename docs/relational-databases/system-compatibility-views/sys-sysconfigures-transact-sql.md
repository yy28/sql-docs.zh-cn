---
title: sys. sysconfigures （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
author: rothja
ms.author: jroth
ms.openlocfilehash: c785ee1c4d3c5382aa42adf48ad9880f00297137
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68089205"
---
# <a name="syssysconfigures-transact-sql"></a>sys. sysconfigures （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对每个由用户设置的配置选项都包含一行。 **sysconfigures**包含在最新启动之前定义的配置选项，以及自[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]那时起设置的任何动态配置选项。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**负值**|**int**|用户可修改的变量值。 仅在执行 RECONFIGURE 后，由[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用。|  
|**config.xml**|**int**|配置变量号。|  
|**条**|**nvarchar(255)**|对配置选项的解释。|  
|**状态值**|**smallint**|指示选项状态的位图。 可能的值包括：<br /><br /> 0 = 静态。 重新启动服务器后，设置才会生效。<br /><br /> 1 = 动态。 执行 RECONFIGURE 语句后，变量才会生效。<br /><br /> 2 = 高级。 仅当设置了 "**显示高级选项**" 时，才会显示变量。 重新启动服务器后，设置才会生效。<br /><br /> 3 = 动态和高级。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;的兼容性视图 &#40;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
