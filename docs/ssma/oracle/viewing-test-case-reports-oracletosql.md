---
title: "查看测试用例报表 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99ee650698adb2536ebdcadf480ae0ccefda2628
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="viewing-test-case-reports-oracletosql"></a>查看测试用例报表 (OracleToSQL)
测试用例报表显示了测试验证结果和常规测试信息。 如果测试失败，还显示有关已验证的对象中的任何不匹配数据的信息。  
  
## <a name="report-structure"></a>报表结构  
报表的顶部显示这些统计信息：  
  
-   经过测试的对象和测试成功的对象数的总数。  
  
-   已验证的表和外键的总数和的表和成功匹配的外键数。  
  
-   开始时间、 结束时间的测试用例和所需执行的总时间。  
  
报表的其余部分显示了四种类别中的信息：  
  
**先决条件错误**  
显示发生了任何错误**先决条件步骤。** 通常情况下，它会跳过。  
  
**初始化**  
显示执行的状态**成功**或**失败**。  
  
**测试对象结果**  
结果 （成功或失败） 和 SSMA 测试人员检测到发生故障时不匹配的比较。  
  
**终止**  
显示执行的状态**成功**或**失败**。  
  
## <a name="see-also"></a>另请参阅  
[运行测试用例 &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[测试迁移数据库对象 &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

