---
title: dbo. sysproxysubsystem （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxysubsystem_TSQL
- dbo.sysproxysubsystem
- sysproxysubsystem_TSQL
- sysproxysubsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxysubsystem system table
ms.assetid: 6d7713f5-1253-4a19-b1fb-635c377c95c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4065c65b8e93d551fcf0af8f2bd242fa71d8d0aa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82806723"
---
# <a name="dbosysproxysubsystem-transact-sql"></a>dbo.sysproxysubsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  记录每个代理帐户所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理子系统。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系统的 ID。 此值对应于**syssubsystems**表中的**subsystem_id**列。|  
|**proxy_id**|**int**|代理帐户的 ID。 此值对应于**sysproxies**表中的**proxy_id**列。|  
  
## <a name="remarks"></a>备注  
 只有**sysadmin**固定服务器角色的成员才能访问此表。  
  
## <a name="see-also"></a>另请参阅  
 [syssubsystems &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)   
 [sysproxies &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
