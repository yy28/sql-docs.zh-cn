---
title: 数据迁移设置 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 573e673e-a194-4cb2-9aba-aaac6e1a225c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7dbdee734d6d8a1dac825ad8f502c5851f746f42
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298881"
---
# <a name="data-migration-settings-db2tosql"></a>数据迁移设置 (DB2ToSQL)
  
## <a name="data-migration-settings"></a>数据迁移设置  
**数据迁移设置**使用户可以编写自定义查询的数据迁移。  
  
-   时，此选项卡才可用**扩展数据迁移选项**设置为**显示**当设置为时将隐藏**隐藏**项目设置中。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移）](https://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae) 。  
  
-   在将实现自定义 SQL 语句的分析**数据迁移设置**表节点的选项卡。  
  
-   以下是中提供两个复选框**数据迁移设置**报道。:  
  
    1.  截断的 SQL Server 表  
  
    2.  使用自定义选择  
  
1.  **截断的 SQL Server 表：**  
     此选项允许用户在目标数据库具有清楚地查看已迁移的数据。  
  
    -   默认情况下，此文本框处于选中状态。  
  
    -   如果未选中此文本框中，则迁移的数据将添加到目标数据库上的现有数据。  
  
2.  **使用自定义选择：**  
     此选项允许用户修改**选择**存在的语句 (**选择**语句，用户可以选择要显示在目标数据库的数据)。  
  
    1.  默认情况下，此文本框为未选中状态。  
  
    2.  如果此文本框处于选中状态，则它允许用户修改**选择**存在的语句。  
  
有两个按钮存在报道。:  
  
-   **应用：** 单击**应用**以应用设置已更改。  
  
-   **取消：** 单击**取消**若要还原的设置存在，就发生了更改。  
  
## <a name="see-also"></a>请参阅  
[将 DB2 数据迁移到 SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b)  
  
