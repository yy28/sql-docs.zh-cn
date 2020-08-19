---
description: MSpublisher_databases (Transact-SQL)
title: MSpublisher_databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7f9b520c283f62bb42a981da746995e33b7b0164
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419081"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  由本地分发服务器提供服务的每个发布服务器/发布服务器数据库对在 **MSpublisher_databases** 表中各占一行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**id**|**int**|行的 ID。|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的版本，可以是下列值之一：<br /><br /> **10** = 个人版<br /><br /> **11** = 桌面引擎 (MSDE) <br /><br /> **20** = 标准<br /><br /> **21** = 工作组<br /><br /> **30** = 企业 (评估) <br /><br /> **31** = 开发人员<br /><br /> **40** = Express (express 不能是发布服务器。 提供此值是为了确保完整性。）|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
