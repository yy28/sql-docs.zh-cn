---
title: 选择并配置测试 (OracleToSQL) 的对象 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e0a8e7650534d50c5e5d7c3b02f2857764d9c2ca
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264642"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>选择并配置要测试的对象 (OracleToSQL)
在此步骤中，选择要测试和配置设置的比较过程的函数的输出参数，以及函数的返回值对象。  
  
## <a name="selection-of-objects-to-test"></a>选择的测试的对象  
在位于左侧和右侧的窗口上 Oracle 对象树中，检查你想要在测试过程中调用的对象。 请参阅中的可测试对象的完整列表[测试迁移的数据库对象&#40;OracleToSQL&#41; ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)主题。  
  
SSMA Tester 不支持任何所选测试对象，如果你将看到标记为链接**有些选定的对象包含错误**在对象树。 单击此链接可查看这些对象为何无法进行测试的原因，从而清除所选的错误的对象。  
  
在右侧可以查看多个页面**SQL**页显示了当前对象的定义。 **参数**页列出了参数，如果对象是存储的过程或函数。 **属性**页显示对象的其他特征。 请参阅的说明**参数的比较**并**调用值**下面的页面。  
  
## <a name="parameter-comparison-settings"></a>参数比较设置  
建立输出参数的比较规则，并返回值中的**参数的比较**页。 可以进行以下设置。  
  
### <a name="use-during-test-comparisons"></a>比较测试期间使用  
启用使用的测试结果比较中选定的参数。  
  
-   如果愿意 **，则返回 True**，SSMA 将 SQL Server 上的相应值在 Oracle 上执行过程后比较此参数的输出值。
  
-   如果愿意**False**，该参数将从结果验证中排除。  
  
### <a name="use-custom-scale"></a>使用自定义缩放  
对于数值数据类型的参数，可以设置用于比较的自定义规模。  
  
-   如果愿意 **，则返回 True**，将根据舍入数字值**比较规模**值之前对它们进行比较。  
  
-   如果愿意**False**，数值比较将是准确。  
  
### <a name="comparing-scale"></a>比较规模  
才可用**使用自定义比例**选项设置为**True**。 这是数值比较的精度。  
  
### <a name="date-time-comparing"></a>日期时间比较  
定义日期/时间值进行比较。  
  
-   如果选择**比较整个日期**，将执行完整比较这两个平台中的值。  
  
-   如果选择**比较仅日期**，将忽略部分的时间。  
  
-   如果选择**比较仅限时间**、 将忽略部分日期。  
  
-   如果选择**忽略毫秒**，最多秒将比较结果。  
  
-   如果选择**忽略日期和毫秒**，结果将是比较仅由时间部分与忽略的一秒的小数部分。  
  
### <a name="ignore-strings-case"></a>忽略字符串大小写  
控制比较的区分大小写。  
  
-   如果愿意 **，则返回 True**，比较将为不区分大小写。  
  
-   如果愿意**False**，该比较将不区分大小写。  
  
### <a name="ignore-trailing-spaces"></a>忽略尾随空格  
控制如何尾随空格将被视为的比较过程。  
  
-   如果愿意 **，则返回 True**，比较的字符串之前，将权限修整比较。  
  
-   如果愿意**False**，比较的字符串将会保留尾随空格。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>指定输入的值的过程和函数 （调用值）  
可以在指定输入的参数值**调用值**页。 **添加调用**按钮将添加新的调用使用空参数值。 **删除调用**按钮删除当前的调用。  
  
## <a name="next-step"></a>下一步  
[选择并配置受影响的对象&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
