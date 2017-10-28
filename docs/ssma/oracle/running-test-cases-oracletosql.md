---
title: "运行测试用例 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d810cee8f3d8b521350aa99a83ca6f7148cd5064
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="running-test-cases-oracletosql"></a>运行测试用例 (OracleToSQL)
SSMA 测试人员运行时测试用例，它将执行测试所选的对象并创建报告，有关验证结果。 如果在这两个平台上完全相同结果，测试成功。 Oracle 之间的对象的对应关系和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]根据当前的 SSMA 项目的架构映射设置确定。  
  
一次成功测试必要要求是 Oracle 的所有对象将转换并加载到目标数据库。 另外，以便同步这两个平台上的表的内容，则应迁移表数据。  
  
## <a name="run-test-case"></a>运行测试用例  
若要运行的已准备的测试用例：  
  
1.  单击**运行**按钮。  
  
2.  在**连接到 Oracle**对话框中，输入连接信息，然后单击**连接**。  
  
测试完成后，创建测试用例报告。 单击**报表**按钮，以查看[测试用例报表](http://msdn.microsoft.com/en-us/8da14323-9dd6-4019-bf79-3e8b972a9bc0)。 测试 （测试用例报告） 的结果会自动存储在[测试结果储存库](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)以供将来使用。  
  
## <a name="test-case-execution-steps"></a>测试用例执行步骤  
  
### <a name="prerequisites"></a>必要條件  
SSMA 测试人员检查是否用于测试的测试执行开始之前满足所有先决条件。 如果未满足某些条件，则将显示一条错误消息。  
  
### <a name="initialization"></a>初始化  
在此步骤中，SSMA 测试人员在 Oracle 服务器的 SSMATESTER_ORACLE 架构中创建辅助对象 （表、 触发器和视图）。 它们允许跟踪中选择以进行验证的受影响对象所做的更改。  
  
假定已验证的表名为 USER_TABLE。 对于此类表中，以下辅助对象是在 Oracle 中创建的。  
  
||||  
|-|-|-|  
|名称|类型|Description|  
|USER_TABLE$ Trg|触发器|审核已验证的表中的更改的触发器。|  
|USER_TABLE$ AUD|table|保存已删除并覆盖的行的表。|  
|USER_TABLE$ AUDID|table|保存新的和已更改行的表。|  
|USER_TABLE|视图|简化的表示形式的表修改。|  
|新 USER_TABLE $|视图|简化的表示形式插入的和被覆盖的行。|  
|USER_TABLE$ NEW_ID|视图|插入的和已更改行的标识。|  
|USER_TABLE$ 旧|视图|简化的表示形式被删除，而且覆盖的行。|  
  
以下对象创建的已验证表的架构中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
||||  
|-|-|-|  
|名称|类型|Description|  
|USER_TABLE$ Trg|触发器|审核已验证的表中的更改的触发器。|  
  
和以下对象创建在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ssmatesterdb 数据库中。  
  
||||  
|-|-|-|  
|名称|类型|Description|  
|USER_TABLE$ Aud|table|保存已删除并覆盖的行的表。|  
|USER_TABLE$ AudID|table|保存新的和已更改行的表。|  
|USER_TABLE|视图|简化的表示形式的表修改。|  
|新的 USER_TABLE $|视图|简化的表示形式插入的和被覆盖的行。|  
|USER_TABLE$ new_id|视图|插入的和已更改行的标识。|  
|旧的 USER_TABLE $|视图|简化的表示形式被删除，而且覆盖的行。|  
  
### <a name="test-object-calls"></a>测试对象调用  
在此步骤中，SSMA 测试人员时，将调用选择用于测试每个对象的结果进行比较并显示报表。  
  
### <a name="finalization"></a>终止  
在终止期间 SSMA 测试人员负责清除在创建的辅助对象**初始化**步骤。  
  
## <a name="next-step"></a>下一步  
[查看测试用例报表 &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>另请参阅  
[选择并配置的对象添加到测试 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[选择并配置受影响对象 &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[测试迁移数据库对象 &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

