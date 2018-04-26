---
title: 使用测试存储库 (OracleToSQL) |Microsoft 文档
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
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 451567181f1963dd049b5dac6bb0177583993e78
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="using-test-repositories-oracletosql"></a>使用测试存储库 (OracleToSQL)
SSMA 测试储存库中存储 SSMA 测试器测试用例和测试结果以供将来使用。 存储库数据保存在 SQL Server 表**TestCaseRepository**和**RunTestCaseResultRepository**架构中**ssma_oracle_utilities**的**ssmatesterdb**数据库。  
  
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
  
-   单击**运行**按钮以打开[运行测试用例 (OracleToSQL)](http://msdn.microsoft.com/en-us/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02)对话框并执行所选的测试。  
  
## <a name="test-results-repository"></a>测试结果储存库  
你可以查看测试结果储存库上**测试结果**页**存储库的测试用例**窗口。 通过单击打开**测试结果...** 从**测试人员**菜单。  
  
你可以使用两个筛选器**测试结果**页：  
  
-   测试用例名称筛选器： 允许选择测试结果的测试用例的名称。 此筛选器的**所有测试用例**值允许显示所有测试用例的测试结果。  
  
-   测试用例执行日期筛选器： 筛选器的日期保存测试结果。此筛选器的**所有段**值允许保存任何日期显示测试结果。  
  
有关测试结果的以下信息显示在网格中。  
  
-   名称： 测试用例的名称。  
  
-   保存： 测试案例的保存的日期。  
  
-   结果: （此单元格的工具提示显示完整的测试执行摘要） 的测试执行的简短摘要。  
  
测试结果页上提供了以下按钮：  
  
-   单击**视图**按钮以打开[查看测试用例报表&#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)的当前的测试用例结果。  
  
-   单击**删除**按钮以删除所选的测试结果  
  
## <a name="see-also"></a>另请参阅  
[运行测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
