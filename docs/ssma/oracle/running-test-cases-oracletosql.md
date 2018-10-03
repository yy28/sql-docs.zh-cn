---
title: 运行测试用例 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 537865967d0e43b7dd9501f9fbb7b9605f5b9367
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696746"
---
# <a name="running-test-cases-oracletosql"></a>运行测试用例 (OracleToSQL)
SSMA 测试人员运行时测试用例，它执行所选测试对象，并创建有关验证结果的报告。 如果结果为在这两个平台上完全相同，测试成功。 Oracle 之间的对象的对应关系和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]根据当前的 SSMA 项目的架构映射设置确定。  
  
成功的测试的一个必要要求是所有 Oracle 对象将转换并加载到目标数据库。 此外，应该迁移表数据，以便同步这两个平台上的表的内容。  
  
## <a name="run-test-case"></a>运行测试用例  
运行已准备好的测试用例：  
  
1.  单击**运行**按钮。  
  
2.  在中**连接到 Oracle**对话框中，输入连接信息，然后单击**Connect**。  
  
测试完成后，创建测试用例报表。 单击**报表**按钮，以查看[测试用例报表](viewing-test-case-reports-oracletosql.md)。 测试 （测试用例报表） 的结果会自动存储在[测试结果储存库](using-test-repositories-oracletosql.md)以供将来使用。  
  
## <a name="test-case-execution-steps"></a>测试用例执行步骤  
  
### <a name="prerequisites"></a>必要條件  
SSMA 测试人员会检查测试的测试执行开始前是否满足所有先决条件。 如果不满足某些条件时，会显示一条错误消息。  
  
### <a name="initialization"></a>初始化  
在此步骤中，SSMA 测试人员在 Oracle 服务器的 SSMATESTER_ORACLE 架构中创建辅助对象 （表、 触发器和视图）。 它们允许跟踪中受影响的对象选择进行验证所做的更改。  
  
假定已验证的表名为 USER_TABLE。 对于此类表，请在 Oracle 中创建以下辅助对象。  
  
||||  
|-|-|-|  
|“属性”|类型|Description|  
|USER_TABLE$ /{trg|触发器|审核已验证的表中的更改的触发器。|  
|USER_TABLE$ 澳大利亚元|表|保存已删除和覆盖的行的表。|  
|USER_TABLE$ AUDID|表|保存新的和已更改行的表。|  
|USER_TABLE|view|表修改简化表示形式。|  
|新 USER_TABLE $|view|简化表示形式插入和覆盖的行。|  
|USER_TABLE$ NEW_ID|view|插入和已更改的行的标识。|  
|USER_TABLE$ 旧|view|已删除和覆盖的行的简化表示形式。|  
  
在已验证表的架构中创建以下对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
||||  
|-|-|-|  
|“属性”|类型|Description|  
|USER_TABLE$ /{trg|触发器|审核已验证的表中的更改的触发器。|  
  
在中创建以下对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ssmatesterdb 数据库中。  
  
||||  
|-|-|-|  
|“属性”|类型|Description|  
|USER_TABLE$ 澳大利亚元|表|保存已删除和覆盖的行的表。|  
|USER_TABLE$ AudID|表|保存新的和已更改行的表。|  
|USER_TABLE|view|表修改简化表示形式。|  
|USER_TABLE $ 新|view|简化表示形式插入和覆盖的行。|  
|USER_TABLE$ new_id|view|插入和已更改的行的标识。|  
|USER_TABLE $ 旧|view|已删除和覆盖的行的简化表示形式。|  
  
### <a name="test-object-calls"></a>测试对象调用  
在此步骤中，SSMA 测试人员调用所选测试每个对象、 比较结果，并显示的报表。  
  
### <a name="finalization"></a>终止  
在终止期间 SSMA 测试人员会清理在创建的辅助对象**初始化**步骤。  
  
## <a name="next-step"></a>下一步  
[查看测试用例报表&#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[选择并配置测试的对象&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[选择并配置受影响的对象&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
