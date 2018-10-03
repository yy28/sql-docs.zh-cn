---
title: 临时表元数据视图和函数 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e5d23ec9-7d18-40f6-add4-bea13132d0b9
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3fec04d1ae381eca3b35c4457510ccd9321caeda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846415"
---
# <a name="temporal-table-metadata-views-and-functions"></a>临时表元数据视图和函数
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 包括多个元数据库视图和函数，可以让管理员检索有关临时表的信息。  
  
 以下元数据视图公开了有关临时表的信息：  
  
-   [sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
-   [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
-   [sys.periods (Transact-SQL)](../../relational-databases/system-catalog-views/sys-periods-transact-sql.md)  
  
 以下元数据函数公开了有关临时表的信息：  
  
-   [OBJECTPROPERTY (Transact-SQL)](../../t-sql/functions/objectproperty-transact-sql.md)  
  
-   [OBJECTPROPERTYEX (Transact-SQL)](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
-   [COLUMNPROPERTY (Transact-SQL)](../../t-sql/functions/columnproperty-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [系统版本控制临时表入门](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [临时表系统一致性检查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [临时表分区](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [临时表注意事项和限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [临时表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系统版本控制临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
  
  
