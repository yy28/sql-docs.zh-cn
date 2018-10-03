---
title: 查看测试用例报表 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 840f73d0732d0789d378c6f1bceb100c58e01bb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624465"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>查看测试用例报表 (SybaseToSQL)
测试用例报表显示的测试验证结果和一般测试的信息。 如果测试失败，还会显示有关已验证的对象中的任何不匹配数据的信息。  
  
## <a name="report-structure"></a>报表结构  
报表的顶部显示了这些统计信息：  
  
-   经过测试的对象和测试成功的对象数的总数。  
  
-   已验证的表和外键的总数和表和成功匹配的外键的数目。  
  
-   开始时间、 结束时间的测试用例和执行所需的总时间。  
  
报表的其余部分显示了四个类别中的信息：  
  
**先决条件错误**  
显示发生了任何错误**先决条件**步骤。 通常情况下，它会跳过。  
  
**初始化**。  
显示的执行情况的状态**成功**或**失败**。  
  
**测试对象结果**  
结果 （成功或失败） 和 SSMA 测试人员检测到发生故障时不匹配的比较。  
  
**终止**  
显示的执行情况的状态**成功**或**失败**。  
  
## <a name="see-also"></a>请参阅  
[运行测试用例&#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
