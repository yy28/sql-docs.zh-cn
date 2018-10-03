---
title: 创建测试用例 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 07b52a71d3f12455bacdd2e9789aadb5ed5967db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604675"
---
# <a name="creating-test-cases-oracletosql"></a>创建测试用例 (OracleToSQL)
使用测试用例向导来创建测试。 此向导允许您通过选择测试并验证对象和指定的测试参数创建测试用例。  
  
## <a name="starting-the-test-case-wizard"></a>启动测试用例向导  
若要启动测试用例向导单击**新建测试用例...** 从**测试人员**菜单。  
  
在启动时，该向导查找架构 SSMATESTER_ORACLE 源 Oracle 服务器上。 它是用于存储辅助对象的测试人员扩展架构。 如果测试用例向导找不到 SSMATESTER_ORACLE，它会显示一个对话框窗口提供了创建架构。 （这种情况下通常发生在首次运行 SSMA 测试人员的过程。）  
  
如果收到对话框窗口中，单击**是**源服务器上创建 SSMATESTER_ORACLE 架构。 请注意，您必须具有 Oracle 权限以创建新用户并在此用户的架构中创建对象。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>创建测试用例使用向导概述  
创建测试用例的过程包括以下五个步骤：  
  
1.  [初始化测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [选择并配置测试的对象&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [选择并配置受影响的对象&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [自定义调用顺序&#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [完成测试用例准备&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
