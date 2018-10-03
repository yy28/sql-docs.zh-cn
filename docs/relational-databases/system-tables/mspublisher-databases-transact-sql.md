---
title: MSpublisher_databases (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7904bd3b6d629daf65d97bf88bba26cbb02bd93f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620745"
---
# <a name="mspublisherdatabases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublisher_databases**表包含每个发布服务器/发布服务器数据库对由本地分发服务器提供服务的一个行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**id**|**int**|行的 ID。|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的版本，可以是下列值之一：<br /><br /> **10** = 个人版<br /><br /> **11** = 桌面引擎 (MSDE)<br /><br /> **20** = 标准<br /><br /> **21** = 工作组<br /><br /> **30** = Enterprise （评估版）<br /><br /> **31** = 开发人员<br /><br /> **40** = express （Express 不能是发布服务器。 提供此值是为了确保完整性。）|  
  
## <a name="see-also"></a>请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
