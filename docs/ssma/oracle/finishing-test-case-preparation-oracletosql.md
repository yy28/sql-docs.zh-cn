---
title: 完成测试用例准备 (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 7b1ca4a9af16b008a1f971541d07069b39f8f9b6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="finishing-test-case-preparation-oracletosql"></a>完成测试用例准备 (OracleToSQL)
向导的最后一页显示的测试用例说明和有关测试中涉及的对象的信息。 此外，在此页上你可以设置测试执行选项。  
  
**测试用例信息**部分显示测试用例的名称和描述。  
  
**对象选择到要测试**部分包含的按对象类型分组的测试对象的命名的列表。  
  
**对象受影响的测试，将分析**部分显示的数据更改应比较后经过测试的对象执行对象的命名的列表。  
  
## <a name="test-case-settings"></a>测试用例设置  
在**测试用例设置**部分可以设置以下执行测试选项：  
  
### <a name="stop-test-execution-after-first-failure"></a>停止后第一次失败的测试执行  
指定要中断测试，如果测试执行过程中发生错误。  
  
-   如果你选择**是**，测试执行中断，如果发生错误。  
  
-   如果你选择**否**，在出错后继续测试执行。  
  
### <a name="perform-data-rollback"></a>执行数据回滚  
测试执行后启用自动数据回滚。  
  
-   如果你选择**是**，在测试执行之后，数据更改都将丢失。  
  
-   如果你选择**否**，执行将保存数据更改的所有测试。  
  
### <a name="auxiliary-tables-saving-mode"></a>保存模式的辅助表  
定义测试执行过程中创建的辅助表的保存模式。 请参阅辅助表中的说明[运行测试用例&#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md)主题。  
  
-   如果你选择**始终将保存**，辅助表数据将始终存储供以后使用。  
  
-   如果你选择**保存如果表比较失败**，仅当发生错误将存储辅助表数据。  
  
-   如果你选择**始终删除**，辅助表始终在测试执行后删除。  
  
-   如果你选择**询问用户如果表比较失败**，用户可以选择必要的操作，如果发生错误。  
  
单击**完成**按钮以保存到已准备的测试用例[使用测试存储库 (OracleToSQL)](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)。  
  
## <a name="see-also"></a>另请参阅  
[使用测试存储库&#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[运行测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
