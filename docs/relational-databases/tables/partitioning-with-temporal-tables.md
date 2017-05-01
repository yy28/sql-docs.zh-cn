---
title: "临时表分区 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0134010294aec01d47271a7e00e6a13e4a3ad208
ms.lasthandoff: 04/11/2017

---
# <a name="partitioning-with-temporal-tables"></a>临时表分区
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  可以单独在当前表和历史记录表上使用分区。 但是，分区不能用于更改数据无系统版本控制的数据内容。  
  
> [!NOTE]  
>  分区是企业版功能。  
  
-   **当前表：**  
  
    -   当**SWITCH IN** 为 **SWITCH IN** 时，当前表的 **SWITCH IN**可用于加快数据加载和查询  
  
    -   **SWITCH OUT** is not permitted while **SYSTEM_VERSIONING** is **ON**  
  
-   **历史记录表：**  
  
    -   当**SWITCH OUT** 为 **SWITCH OUT** 时，可以执行历史记录表中的 **SWITCH OUT** to purge portions of h时，可以执行历史记录表中的tory data that 时，可以执行历史记录表中的 no longer relevant.  
  
    -   当**SWITCH IN** 为 **SWITCH IN** 时，不允许执行 **SWITCH IN** since it can invalidate temporal data cons时，不允许执行tency.  
  
## <a name="did-this-article-help-you-were-listening"></a>本文是否对你有帮助？ 我们洗耳恭听  
 你正在查找哪些信息，是否已经找到？ 我们不断听取你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Partitioning%20with%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>另请参阅  
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [系统版本控制临时表入门](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [临时表系统一致性检查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [临时表注意事项和限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [临时表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系统版本控制临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [临时表元数据视图和函数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

