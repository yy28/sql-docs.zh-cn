---
title: 查看测试用例报表 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 423726112ce1746695f2ee61f2c2668489b26555
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="viewing-test-case-reports-sybasetosql"></a>查看测试用例报表 (SybaseToSQL)
测试用例报表显示了测试验证结果和常规测试信息。 如果测试失败，还显示有关已验证的对象中的任何不匹配数据的信息。  
  
## <a name="report-structure"></a>报表结构  
报表的顶部显示这些统计信息：  
  
-   经过测试的对象和测试成功的对象数的总数。  
  
-   已验证的表和外键的总数和的表和成功匹配的外键数。  
  
-   开始时间、 结束时间的测试用例和所需执行的总时间。  
  
报表的其余部分显示了四种类别中的信息：  
  
**先决条件错误**  
显示发生了任何错误**先决条件**步骤。 通常情况下，它会跳过。  
  
**初始化**。  
显示执行的状态**成功**或**失败**。  
  
**测试对象结果**  
结果 （成功或失败） 和 SSMA 测试人员检测到发生故障时不匹配的比较。  
  
**终止**  
显示执行的状态**成功**或**失败**。  
  
## <a name="see-also"></a>另请参阅  
[运行测试用例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
