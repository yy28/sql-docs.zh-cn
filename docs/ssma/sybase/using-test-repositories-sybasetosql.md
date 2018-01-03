---
title: "使用测试存储库 (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef959c05f397a898d9c1e72adddd6b895eabf87d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="using-test-repositories-sybasetosql"></a>使用测试存储库 (SybaseToSQL)
SSMA 测试储存库中存储 SSMA 测试器测试用例和测试结果以供将来使用。 存储库数据保存在 SQL Server 表**TestCaseRepository**和**RunTestCaseResultRepository**架构中**ssma_sybase_utilities**的**ssmatesterdb_syb**数据库。  
  
在存储库的测试用例对话框中有以下按钮：  
  
-   单击**刷新**按钮以刷新测试用例或测试结果列表。  
  
-   单击**关闭**按钮以关闭存储库的测试用例对话框。  
  
## <a name="test-cases-repository"></a>测试用例存储库  
你可以通过单击查看测试用例存储库**测试用例...** 从**测试人员**菜单。 SSMA 然后显示**存储库的测试用例**对话框窗口上的已保存测试用例的列表**测试用例**页。  
  
该网格显示有关每个测试用例的以下信息：  
  
-   名称： 测试用例名称。  
  
-   创建： 测试用例创建日期。  
  
-   修改： 测试用例上次修改日期。  
  
-   描述： 测试用例说明。  
  
测试用例页上提供了以下按钮：  
  
-   单击**添加**按钮以运行测试用例向导并创建新的测试。  
  
-   单击**删除**按钮从存储库中删除所选的测试。当删除测试用例时，也将删除所有相关的测试结果。  
  
-   单击**编辑**按钮以运行测试用例向导并更改所选的测试。  
  
-   单击**运行**按钮以打开[运行测试用例 &#40;SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)对话框并执行所选的测试。  
  
## <a name="test-results-repository"></a>测试结果储存库  
你可以查看测试结果储存库上**测试结果**页**存储库的测试用例**窗口。 通过单击打开**测试结果...** 从**测试人员**菜单。  
  
你可以使用两个筛选器**测试结果**页：  
  
-   测试用例名称筛选器： 允许选择测试结果的测试用例的名称。 此筛选器的**所有测试用例**值允许显示所有测试用例的测试结果。  
  
-   测试用例执行日期筛选器： 筛选器的日期保存测试结果。此筛选器的**所有段**值允许保存任何日期显示测试结果。  
  
有关测试结果的以下信息显示在网格中。  
  
-   名称： 测试用例的名称。  
  
-   启动： 测试案例的运行日期。  
  
-   结果: （此单元格的工具提示显示完整的测试执行摘要） 的测试执行的简短摘要。  
  
测试结果页上提供了以下按钮：  
  
-   单击**视图**按钮以打开[查看测试用例报表 &#40;SybaseToSQL &#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)的当前的测试用例结果。  
  
-   单击**删除**按钮以删除所选的测试结果  
  
## <a name="see-also"></a>另请参阅  
[运行测试用例 &#40;SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[测试迁移数据库对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
