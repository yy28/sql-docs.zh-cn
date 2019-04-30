---
title: 完成测试用例准备 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1bdbe8616f5f2c3252f813e6e2636966ff16ec16
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288531"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>完成测试用例准备 (OracleToSQL)
向导的最后一页显示的测试用例说明和测试中涉及的对象的信息。 此外，在此页上，可以设置测试执行选项。  
  
**测试用例信息**部分显示测试用例的名称和说明。  
  
**对象所选为要测试**部分包含按对象类型分组的测试对象的命名的列表。  
  
**对象会受到影响的测试，则会分析**部分显示的数据更改应在经过测试的对象执行之后比较的对象的命名的列表。  
  
## <a name="test-case-settings"></a>测试用例设置  
在中**测试用例设置**部分可以设置以下执行测试选项：  
  
### <a name="stop-test-execution-after-first-failure"></a>停止后第一次失败的测试执行  
指定要在测试执行期间发生错误的情况下会中断测试。  
  
-   如果愿意**是**，测试执行分页符，如果发生错误。  
  
-   如果愿意**否**，出现错误后继续测试执行。  
  
### <a name="perform-data-rollback"></a>执行数据回滚  
测试执行后启用自动数据回滚。  
  
-   如果愿意**是**，在测试执行之后，数据更改都将丢失。  
  
-   如果愿意**否**，所有测试的执行将保存数据更改。  
  
### <a name="auxiliary-tables-saving-mode"></a>辅助表格保存模式  
定义测试执行过程中创建的辅助表的保存模式。 请参阅辅助表中的说明[运行测试用例&#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md)主题。  
  
-   如果选择**始终保存**，辅助表数据将始终存储供以后使用。  
  
-   如果选择**如果表的比较失败，则保存**，仅当发生错误，将存储辅助表数据。  
  
-   如果选择**始终删除**，辅助表格始终在测试执行之后删除。  
  
-   如果选择**如果表的比较失败，则要求用户**，用户可以选择必要的操作，如果发生错误。  
  
单击**完成**按钮以保存到已准备好的测试用例[使用测试存储库 (OracleToSQL)](https://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)。  
  
## <a name="see-also"></a>请参阅  
[使用测试存储库&#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[运行测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
