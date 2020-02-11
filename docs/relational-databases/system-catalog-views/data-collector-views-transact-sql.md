---
title: 数据收集器视图（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- data collector [SQL Server], views
ms.assetid: a005e885-7813-4c7e-b332-b01d9e9d4054
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9e412f796a5b04f980557b5a3131763811aa78da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68033168"
---
# <a name="data-collector-views-transact-sql"></a>数据收集器视图 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  数据收集器可提供以下视图，用于显示有关数据收集器配置的信息（如收集器类型属性、收集组和收集组项）以及收集组运行时获得的执行统计信息。 这些视图位于**msdb**数据库中，也为基础表提供抽象层。 这种抽象化通过禁止对表的直接访问，同时允许在不影响任何关联应用程序的情况下对表进行更改，使安全性得以提高。  
  
|||  
|-|-|  
|[syscollector_collection_items &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|[syscollector_collection_sets &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|  
|[syscollector_collector_types &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|[syscollector_config_store &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|  
|[syscollector_execution_log &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|[syscollector_execution_log_full &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|  
|[syscollector_execution_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)||  
  
## <a name="see-also"></a>另请参阅  
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
