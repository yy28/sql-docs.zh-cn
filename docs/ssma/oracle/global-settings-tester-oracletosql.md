---
title: 全局设置 （测试人员） (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4acc0f2a-85ba-4c99-856a-89030f5c418e
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 541be9baa654371e6e5aaca18c91e860d058c7fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="global-settings-tester-oracletosql"></a>全局设置 （测试人员） (OracleToSQL)
使用的测试人员页**全局设置**对话框中指定的 SSMA 测试人员的设置。  
  
若要访问的测试人员设置中，在**工具**菜单上，选择**全局设置**，然后单击**测试人员**在左窗格的底部。  
  
## <a name="options"></a>选项  
**可测试的对象的分析**  
此设置指定是否执行可测试的对象的分析。 选择**是**如果希望 SSMA 测试来分析和自动检查依赖对象。 默认选项集是**是**。  
  
将此设置提供以下选项：  
  
1.  是  
  
2.  否  
  
**保存模式的辅助表**  
此设置指定如何将保存测试用例执行期间创建的内部辅助表。 为此特定设置，可以设置以下选项：  
  
1.  始终删除  
  
2.  始终将保存  
  
3.  如果表比较失败的保存  
  
4.  要求用户是否表比较失败  
  
默认选项集是：**始终删除**。  
  
**执行数据回滚**  
此设置指定是否执行了回滚操作后运行每个测试用例。 默认选项集是**否**。  
  
将此设置提供以下选项：  
  
1.  是  
  
2.  否  
  
**停止后第一次失败的测试执行**  
此设置指定是否停止当前正在运行测试用例，如果执行时出错。 默认选项集是**是**。  
  
将此设置提供以下选项：  
  
1.  是  
  
2.  否  
  
## <a name="see-also"></a>另请参阅  
[完成测试用例准备&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
