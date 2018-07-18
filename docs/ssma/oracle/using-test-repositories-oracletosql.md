---
title: 使用测试存储库 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 863fee753776b0e86408d6ccd0d9d7e0cfc7f33b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979739"
---
# <a name="using-test-repositories-oracletosql"></a>使用测试存储库 (OracleToSQL)
SSMA 测试存储库存储 SSMA 测试人员的测试用例和测试结果以供将来使用。 存储库数据保存在 SQL Server 表**TestCaseRepository**并**RunTestCaseResultRepository**架构中**ssma_oracle_utilities** 的**ssmatesterdb**数据库。  
  
在存储库的测试用例对话框上提供了以下按钮：  
  
-   单击**刷新**按钮以刷新的测试用例或测试结果列表。  
  
-   单击**关闭**按钮以关闭测试用例存储库对话框。  
  
## <a name="test-cases-repository"></a>测试用例存储库  
可以通过单击查看测试用例存储库**测试用例...** 从**测试人员**菜单。 然后显示 SSMA**存储库的测试用例**上的已保存测试用例的列表的对话框窗口**测试用例**页。  
  
该网格将显示有关每个测试用例的以下信息：  
  
-   名称： 测试用例名称。  
  
-   创建： 测试用例的创建日期。  
  
-   已修改： 测试用例的上次修改日期。  
  
-   说明： 测试用例描述。  
  
测试用例页上提供了以下按钮：  
  
-   单击**添加**按钮以运行测试用例向导并创建新的测试。  
  
-   单击**删除**按钮以从存储库中删除所选的测试。删除测试用例时，也会删除所有相关的测试结果。  
  
-   单击**编辑**按钮以运行测试用例向导并更改所选的测试。  
  
-   单击**运行**按钮以打开[运行测试用例 (OracleToSQL)](http://msdn.microsoft.com/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02)对话框并执行所选的测试。  
  
## <a name="test-results-repository"></a>测试结果储存库  
您可以查看测试结果储存库上**测试结果**页**存储库的测试用例**窗口。 通过单击打开**测试结果...** 从**测试人员**菜单。  
  
可以使用两个筛选器**测试结果**页：  
  
-   测试用例名称筛选器： 允许选择测试结果的测试用例的名称。 此筛选器**所有测试用例**值，则允许显示所有测试用例的测试结果。  
  
-   测试用例执行日期筛选器： 筛选器的日期保存测试结果。此筛选器**所有段**值，则允许任何日期保存显示测试结果。  
  
有关测试结果的以下信息显示在网格中。  
  
-   名称： 测试用例的名称。  
  
-   保存： 测试案例的保存的日期。  
  
-   结果: （此单元格的工具提示显示测试执行的完整摘要） 的测试执行的简短摘要。  
  
测试结果页上提供了以下按钮：  
  
-   单击**视图**按钮以打开[查看测试用例报表&#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)当前测试用例结果。  
  
-   单击**删除**按钮可删除所选的测试结果  
  
## <a name="see-also"></a>请参阅  
[运行测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
