---
title: 运行测试用例 (SybaseToSQL) |Microsoft 文档
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
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 687fa8b221a31e0c1c447b5c5cbee85cc31d1702
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="running-test-cases-sybasetosql"></a>运行测试用例 (SybaseToSQL)
SSMA 测试人员运行时测试用例，它将执行测试所选的对象并创建报告，有关验证结果。 如果在这两个平台上完全相同结果，测试成功。 Sybase 之间的对象的对应关系和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]根据当前的 SSMA 项目的架构映射设置确定。  
  
一次成功测试必要要求是所有 Sybase 对象将转换并加载到目标数据库。 另外，以便同步这两个平台上的表的内容，则应迁移表数据。  
  
## <a name="run-test-case"></a>运行测试用例  
若要运行的已准备的测试用例：  
  
1.  单击**运行**按钮。  
  
2.  在**连接到 Sybase**对话框中，输入连接信息，然后单击**连接**。  
  
测试完成后，创建测试用例报告。 单击**报表**按钮，以查看[查看测试用例报表&#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)。 测试 （测试用例报告） 的结果会自动存储在[使用测试存储库&#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md)以供将来使用。  
  
## <a name="test-case-execution-steps"></a>测试用例执行步骤  
  
### <a name="prerequisites"></a>必要條件  
SSMA 测试人员检查是否用于测试的测试执行开始之前满足所有先决条件。 如果未满足某些条件，则将显示一条错误消息。  
  
### <a name="initialization"></a>初始化  
在此步骤中，SSMA 测试人员创建辅助对象 （表、 触发器和视图） 这两个在 Sybase 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 它们允许跟踪表比较模式是否为验证选择受影响表中所做的更改**仅更改**。  
  
假定已验证的表名为 USER_TABLE。 对于此类表中，在 Sybase 创建以下辅助对象。  
  
以下对象创建在 Sybase SSMATESTER2005db 或 SSMATESTER2008db 数据库中和在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ssmatesterdb_syb 数据库中。  
  
|名称|类型|Description|  
|--------|--------|---------------|  
|USER_TABLE$Trg|触发器|审核已验证的表中的更改的触发器。|  
|USER_TABLE$ Aud|表|保存已删除并覆盖的行的表。|  
|USER_TABLE$AudID|表|保存新的和已更改行的表。|  
|USER_TABLE|视图|简化的表示形式的表修改。|  
|新的 USER_TABLE $|视图|简化的表示形式插入的和被覆盖的行。|  
|USER_TABLE$new_id|视图|插入的和已更改行的标识。|  
|USER_TABLE$old|视图|简化的表示形式被删除，而且覆盖的行。|  
  
以下对象创建的数据库中的已验证表 Sybase 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
|名称|类型|Description|  
|--------|--------|---------------|  
|USER_TABLE$Trg|触发器|审核已验证的表中的更改的触发器。|  
  
### <a name="test-object-calls"></a>测试对象调用  
在此步骤中，SSMA 测试人员时，将调用选择用于测试每个对象的结果进行比较并显示报表。  
  
### <a name="finalization"></a>终止  
在终止期间 SSMA 测试人员负责清除在创建的辅助对象**初始化**步骤。  
  
## <a name="next-step"></a>下一步  
[查看测试用例报表&#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[选择并配置的对象添加到测试&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[选择并配置受影响的对象&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
