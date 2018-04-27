---
title: 数据迁移设置 (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 38f4de40b7d581f33c2fe5bce4211d5c7873f900
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="data-migration-settings-oracletosql"></a>数据迁移设置 (OracleToSQL)
  
## <a name="data-migration-settings"></a>数据迁移设置  
**数据迁移设置**允许用户编写自定义查询对于数据迁移。  
  
-   时，此选项卡才可用**扩展数据迁移选项**设置为**显示**并且当设置为时隐藏**隐藏**项目设置。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60) 。  
  
-   将在中实现的自定义 SQL 语句的分析**数据迁移设置**表节点的选项卡。  
  
-   以下是两个中提供的复选框**数据迁移设置**viz。:  
  
    1.  截断的 SQL Server 表  
  
    2.  使用自定义选择  
  
1.  **截断的 SQL Server 表：**  
     此选项允许用户在目标数据库已迁移的数据的清除视图。  
  
    -   默认情况下，会检查此文本框。  
  
    -   如果未选中此文本框中，则迁移的数据将添加到在目标数据库的现有数据。  
  
2.  **使用自定义选择：**  
     此选项允许用户修改**选择**语句存在 (**选择**语句允许用户选择要显示在目标数据库的数据)。  
  
    1.  默认情况下，此文本框为未选中状态。  
  
    2.  如果选中此文本框中，则它允许用户修改**选择**存在的语句。  
  
有两个按钮存在 viz。:  
  
-   **应用：**单击**应用**将已更改的设置。  
  
-   **取消:** 单击**取消**之前进行的更改已还原存在的设置。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据迁移到 SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)  
  
