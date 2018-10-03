---
title: 全局设置 （测试程序） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5d9bf2a94146739a743fc4c310ece1d9c4642d11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607185"
---
# <a name="global-settings-tester-sybasetosql"></a>全局设置（测试程序）(SybaseToSQL)
使用的测试人员页面**全局设置**对话框来指定 SSMA 测试人员的设置。  
  
若要访问测试人员设置中，在**工具**菜单中，选择**全局设置**，然后单击**测试人员**在左窗格的底部。  
  
## <a name="options"></a>选项  
**可测试对象的分析**  
此设置指定是否执行可测试对象的分析。 选择**是**如果你想 SSMA 测试人员来分析和自动检查依赖对象。 默认选项集是**是**。  
  
此设置有以下选项：  
  
1.  用户帐户控制  
  
2.  否  
  
**辅助表格保存模式**  
此设置指定如何将保存测试用例执行期间创建的内部辅助表。 为此特定设置，可以设置以下选项：  
  
1.  始终删除  
  
2.  始终保存  
  
3.  如果表的比较失败，则保存  
  
4.  要求用户是否失败，表的比较  
  
默认选项集是：**始终删除**。  
  
**执行数据回滚**  
此设置指定是否执行回滚操作后运行每个测试用例。 默认选项集是**否**。  
  
此设置有以下选项：  
  
1.  用户帐户控制  
  
2.  否  
  
**停止后第一次失败的测试执行**  
此设置指定是否要停止当前正在运行测试用例，如果执行时出错。 默认选项集是**是**。  
  
此设置有以下选项：  
  
1.  用户帐户控制  
  
2.  否  
  
## <a name="see-also"></a>请参阅  
[完成测试用例准备&#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
