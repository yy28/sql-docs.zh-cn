---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61aa34e8e5b47b50791c8d325afff7698ddd0047
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8649|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|COST_TOO_HIGH|  
|消息正文|查询已取消，因为此查询的估计开销 (%d) 出了配置的阈值 %d。 请与系统管理员联系。|  
  
## <a name="explanation"></a>解释  
查询已取消，因为此查询的估计开销超出了为 QUERY_GOVERNOR_COST_LIMIT 设置的配置阈值。  
  
## <a name="user-action"></a>用户操作  
将 QUERY_GOVERNOR_COST_LIMIT 选项设置为更大的值。  
  
## <a name="see-also"></a>另请参阅  
[SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
