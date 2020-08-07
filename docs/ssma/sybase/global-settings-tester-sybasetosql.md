---
title: 全局设置 (测试人员)  (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f1ebf6d1122db6b28b13c33320dabef520a40f5a
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931284"
---
# <a name="global-settings-tester-sybasetosql"></a>全局设置（测试程序）(SybaseToSQL)
使用 "**全局设置**" 对话框的 "测试器" 页可以指定 SSMA 测试器的设置。  
  
若要访问测试人员设置，请在 "**工具**" 菜单上选择 "**全局设置**"，然后单击左窗格底部的 "**测试**器"。  
  
## <a name="options"></a>选项  
**可测试对象分析**  
此设置指定是否对可测试对象进行分析。 如果希望 SSMA 测试人员分析和自动检查依赖对象，请选择 **"是"** 。 默认选项设置为 **"是"**。  
  
此设置可使用以下选项：  
  
1.  是  
  
2.  否  
  
**辅助表保存模式**  
此设置指定如何保存在执行测试用例的过程中创建的内部辅助表。 可以为此特定设置设置以下选项：  
  
1.  始终删除  
  
2.  始终保存  
  
3.  如果表比较失败，保存  
  
4.  询问用户表比较失败  
  
默认选项设置为：**始终删除**。  
  
**执行数据回滚**  
此设置指定在运行每个测试用例后是否执行回滚操作。 默认选项设置为 "**否**"。  
  
此设置可使用以下选项：  
  
1.  是  
  
2.  否  
  
**在第一次失败后停止测试执行**  
此设置指定是否在执行期间发生错误时停止当前正在运行的测试用例。 默认选项设置为 **"是"**。  
  
此设置可使用以下选项：  
  
1.  是  
  
2.  否  
  
## <a name="see-also"></a>另请参阅  
[完成测试用例准备 &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
