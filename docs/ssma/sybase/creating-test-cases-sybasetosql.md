---
title: 创建测试用例 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: b3f54a38ae995dd2c83fd36647393f81b802fde2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948452"
---
# <a name="creating-test-cases-sybasetosql"></a>创建测试用例 (SybaseToSQL)
使用测试用例向导来创建测试。 此向导允许您通过选择测试并验证对象和指定的测试参数创建测试用例。  
  
## <a name="starting-the-test-case-wizard"></a>启动测试用例向导  
若要启动测试用例向导单击**新建测试用例...** 从**测试人员**菜单。  
  
在启动时，向导将查找数据库 ssmatester2005db 或 ssmatester2008db （具体取决于项目类型） 源 Sybase 服务器上。 它是用于存储辅助对象的测试人员扩展架构。 如果测试用例向导找不到 ssmatester2005db 或 ssmatester2008db，会显示一个对话框窗口提供了创建测试人员扩展数据库。 （这种情况下通常发生在首次运行 SSMA 测试人员的过程。）  
  
如果收到对话框窗口中，单击**是**源服务器上创建 Sybase 测试人员数据库。 然后将出现一个新的对话框窗口，您应在其中添加在其中查找新的测试人员数据库上的一个或多个设备。 单击**添加**添加设备。 在中**测试人员数据库的分配空间**对话框中选择该设备，并指定使用由测试人员数据库的大小。 此外，可以设置适用于数据库日志的单独设备。 请注意，必须具有 Sybase 的特权来创建数据库。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>创建测试用例使用向导概述  
创建测试用例的过程包括以下五个步骤：  
  
1.  [初始化测试用例&#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md)。  
  
2.  [选择并配置测试的对象&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)。  
  
3.  [选择并配置受影响的对象&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)。  
  
4.  [自定义调用顺序&#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)。  
  
5.  [完成测试用例准备&#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)。  
  
## <a name="see-also"></a>请参阅  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
