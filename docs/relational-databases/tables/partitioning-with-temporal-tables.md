---
title: 临时表分区 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c97854b8b9264c7bd52cbb24cc3ac7ae90c8609
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="partitioning-with-temporal-tables"></a>临时表分区
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  可以单独在当前表和历史记录表上使用分区。 但是，分区不能用于更改数据无系统版本控制的数据内容。  
  
> [!NOTE]  
>  分区是在 Service Pack 1 之前以及早期版本的 SQL Server 2016 中的 Enterprise Edition 功能。 在 SQL Server 2016 Service Pack 1 及更高版本的所有版本中都支持分区。
  
-   **当前表：**  
  
    -   当**SWITCH IN** 为 **SWITCH IN** 时，当前表的 **SWITCH IN**可用于加快数据加载和查询  
  
    -   **SYSTEM_VERSIONING** 为 **ON** 时，当前表的 **SWITCH IN**  
  
-   **历史记录表：**  
  
    -   当**SWITCH OUT** 为 **SWITCH OUT** 时，可以执行历史记录表中的 **SWITCH OUT** to purge portions of h时，可以执行历史记录表中的tory data that 时，可以执行历史记录表中的 no longer relevant.  
  
    -   当**SWITCH IN** 为 **SWITCH IN** 时，不允许执行 **SWITCH IN** since it can invalidate temporal data cons时，不允许执行tency.  
  
## <a name="see-also"></a>另请参阅  
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [系统版本控制临时表入门](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [临时表系统一致性检查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [临时表注意事项和限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [临时表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系统版本控制的临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [临时表元数据视图和函数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
