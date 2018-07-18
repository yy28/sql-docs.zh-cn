---
title: 数据迁移设置 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a5590adadc1436d616d73b275ad90359b6e64d88
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984599"
---
# <a name="data-migration-settings-mysqltosql"></a>数据迁移设置 (MySQLToSQL)
  
## <a name="data-migration-settings"></a>数据迁移设置  
**数据迁移设置**使用户可以编写自定义查询的数据迁移。  
  
-   时，此选项卡才可用**扩展数据迁移选项**设置为**显示**当设置为时将隐藏**隐藏**项目设置中。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9) 。  
  
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
  
-   **取消:** 单击**取消**若要还原的设置存在，就发生了更改。  
  
## <a name="see-also"></a>请参阅  
[将 MySQL 数据迁移到 SQL Server/SQL Azure](http://msdn.microsoft.com/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  
