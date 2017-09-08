---
title: "全局设置 （测试人员） (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 21178ca7326678504244658192d7395bab79a9ac
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="global-settings-tester-sybasetosql"></a>全局设置 （测试人员） (SybaseToSQL)
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
[完成测试用例准备 &#40;SybaseToSQL &#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  

