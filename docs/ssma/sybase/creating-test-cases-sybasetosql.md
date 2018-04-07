---
title: 创建测试用例 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0647f807a6a28eb1dc450d3e38b2e591f1b51dd2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="creating-test-cases-sybasetosql"></a>创建测试用例 (SybaseToSQL)
使用测试用例向导来创建测试。 此向导允许您通过选择测试和验证对象和指定的测试参数创建测试用例。  
  
## <a name="starting-the-test-case-wizard"></a>启动测试用例向导  
若要启动的测试用例向导，单击**新测试用例...** 从**测试人员**菜单。  
  
启动时，此向导会查找数据库 ssmatester2005db 或 ssmatester2008db （具体取决于项目类型中） 源 Sybase 服务器上。 它是用于存储辅助对象的测试人员扩展架构。 如果测试用例向导找不到 ssmatester2005db 或 ssmatester2008db，它会显示一个对话框窗口，建议创建的测试人员扩展数据库。 （这种情况下通常发生在 SSMA 测试人员的首次运行过程。）  
  
如果你收到对话框窗口中，单击**是**在源服务器上创建 Sybase 测试人员数据库。 然后将出现一个新的对话框窗口，您应在其中添加在其找到新的测试人员数据库上的一个或多个设备。 单击**添加**来添加设备。 在**测试人员数据库的分配空间**对话框中选择该设备，并指定测试人员数据库使用的大小。 此外，你可以设置数据库日志的单独设备。 请注意，你必须具有 Sybase 特权，无法创建数据库。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>创建测试用例使用向导概述  
创建测试用例的过程包括五个步骤：  
  
1.  [初始化测试用例&#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md)。  
  
2.  [选择并配置的对象添加到测试&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)。  
  
3.  [选择并配置受影响的对象&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)。  
  
4.  [自定义调用顺序&#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)。  
  
5.  [完成测试用例准备&#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
