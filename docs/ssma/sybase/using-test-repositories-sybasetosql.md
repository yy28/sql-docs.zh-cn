---
title: 使用测试存储库 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 939342a85ed657faa645c593018cbf39042031c2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625824"
---
# <a name="using-test-repositories-sybasetosql"></a>使用测试存储库 (SybaseToSQL)
SSMA 测试存储库存储 SSMA 测试人员的测试用例和测试结果以供将来使用。 存储库数据保存在 SQL Server 表**TestCaseRepository**并**RunTestCaseResultRepository**架构中**ssma_sybase_utilities** 的**ssmatesterdb_syb**数据库。  
  
在存储库的测试用例对话框上提供了以下按钮：  
  
-   单击**刷新**按钮以刷新的测试用例或测试结果列表。  
  
-   单击**关闭**按钮以关闭测试用例存储库对话框。  
  
## <a name="test-cases-repository"></a>测试用例存储库  
可以通过单击查看测试用例存储库**测试用例...** 从**测试人员**菜单。 然后显示 SSMA**存储库的测试用例**上的已保存测试用例的列表的对话框窗口**测试用例**页。  
  
该网格将显示有关每个测试用例的以下信息：  
  
-   名称：测试用例的名称。  
  
-   创建：测试用例创建日期。  
  
-   修订日期：测试用例的上次修改日期。  
  
-   说明:测试用例说明中。  
  
测试用例页上提供了以下按钮：  
  
-   单击**添加**按钮以运行测试用例向导并创建新的测试。  
  
-   单击**删除**按钮以从存储库中删除所选的测试。删除测试用例时，也会删除所有相关的测试结果。  
  
-   单击**编辑**按钮以运行测试用例向导并更改所选的测试。  
  
-   单击**运行**按钮以打开[运行测试用例&#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md)对话框并执行所选的测试。  
  
## <a name="test-results-repository"></a>测试结果储存库  
您可以查看测试结果储存库上**测试结果**页**存储库的测试用例**窗口。 通过单击打开**测试结果...** 从**测试人员**菜单。  
  
可以使用两个筛选器**测试结果**页：  
  
-   测试用例名称筛选器：允许选择测试结果的测试用例的名称。 此筛选器**所有测试用例**值，则允许显示所有测试用例的测试结果。  
  
-   测试用例执行日期筛选器：筛选器的日期保存测试结果。此筛选器**所有段**值，则允许任何日期保存显示测试结果。  
  
有关测试结果的以下信息显示在网格中。  
  
-   名称：测试用例的名称。  
  
-   开始：测试用例的正在运行的日期。  
  
-   结果：（此单元格的工具提示显示测试执行的完整摘要） 的测试执行的简短摘要。  
  
测试结果页上提供了以下按钮：  
  
-   单击**视图**按钮以打开[查看测试用例报表&#40;SybaseToSQL&#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)当前测试用例结果。  
  
-   单击**删除**按钮可删除所选的测试结果  
  
## <a name="see-also"></a>请参阅  
[运行测试用例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
