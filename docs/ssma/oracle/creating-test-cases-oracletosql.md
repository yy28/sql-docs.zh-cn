---
title: "创建测试用例 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: fed434b32dd482dfb5700c3b547b7e6016ca9669
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="creating-test-cases-oracletosql"></a>创建测试用例 (OracleToSQL)
使用测试用例向导来创建测试。 此向导允许您通过选择测试和验证对象和指定的测试参数创建测试用例。  
  
## <a name="starting-the-test-case-wizard"></a>启动测试用例向导  
若要启动的测试用例向导，单击**新测试用例...** 从**测试人员**菜单。  
  
启动时，该向导查找架构 SSMATESTER_ORACLE 源 Oracle 服务器上。 它是用于存储辅助对象的测试人员扩展架构。 如果测试用例向导找不到 SSMATESTER_ORACLE，它将显示一个对话框窗口，建议创建架构。 （这种情况下通常发生在 SSMA 测试人员的首次运行过程。）  
  
如果你收到对话框窗口中，单击**是**若要在源服务器上创建 SSMATESTER_ORACLE 架构。 请注意，你必须创建一个新用户和的此用户的架构中创建对象 Oracle 特权。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>创建测试用例使用向导概述  
创建测试用例的过程包括五个步骤：  
  
1.  [初始化测试用例 &#40; OracleToSQL &#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [选择并配置的对象添加到测试 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [选择并配置受影响对象 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [自定义调用顺序 &#40; OracleToSQL &#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [完成测试用例准备 &#40; OracleToSQL &#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>另请参阅  
[测试迁移数据库对象 &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
