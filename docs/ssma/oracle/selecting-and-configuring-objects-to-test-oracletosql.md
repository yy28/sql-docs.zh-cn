---
title: 选择并配置的对象添加到测试 (OracleToSQL) |Microsoft 文档
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
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 2186b7c2e52cbba438dd48b32a2f884e3ccf04fb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>选择并配置的对象添加到测试 (OracleToSQL)
在此步骤中，您将选择对象进行测试，以及如何用于比较过程的和函数的输出参数，以及函数的返回值配置设置。  
  
## <a name="selection-of-objects-to-test"></a>选择向测试的对象  
在位于窗口左侧 Oracle 对象树中，检查你想要在测试过程中调用的对象。 请参阅中的可测试对象的完整列表[测试迁移的数据库对象&#40;OracleToSQL&#41; ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)主题。  
  
如果 SSMA Tester 不支持任何选定的测试对象，你将看到该链接标记为**某些所选的对象包含错误**下对象树。 单击此链接来查看为什么是这些对象不能测试的原因并清除所选内容的错误的对象。  
  
在右侧，你可以查看多个页面**SQL**页显示当前对象的定义。 **参数**页列出了参数，如果对象是存储的过程或函数。 **属性**页显示的对象的其他特征。 请参阅说明**参数比较**和**调用值**下面的页面。  
  
## <a name="parameter-comparison-settings"></a>参数比较设置  
建立输出参数的比较规则和返回值中的**参数比较**页。 你可以进行以下设置。  
  
### <a name="use-during-test-comparisons"></a>在比较测试期间使用  
启用使用的测试结果比较中的所选参数。  
  
-   如果你选择**True**，SSMA 对 Oracle 执行过程，与 SQL Server 上的相应值后将比较此参数的输出值。
  
-   如果你选择**False**，参数将从结果验证中排除。  
  
### <a name="use-custom-scale"></a>使用自定义比例  
对于数值数据类型的参数，可以设置自定义比例进行比较。  
  
-   如果你选择**True**，将根据舍入数字值**比较缩放**值之前对它们进行比较。  
  
-   如果你选择**False**，数值的比较将是准确。  
  
### <a name="comparing-scale"></a>比较缩放  
才可用**使用自定义比例**选项设置为**True**。 这是数值比较的精度。  
  
### <a name="date-time-comparing"></a>日期时间比较  
定义如何日期/时间值进行比较。  
  
-   如果你选择**比较整个日期**，将执行完整比较这两个平台中的值。  
  
-   如果你选择**仅比较日期**，将忽略部分的时间。  
  
-   如果你选择**仅比较时间**、 将忽略部分的日期。  
  
-   如果你选择**忽略毫秒**，结果将比较最秒。  
  
-   如果你选择**忽略日期和毫秒**，结果将是比较仅由时间部分和忽略小数部分的第二个。  
  
### <a name="ignore-strings-case"></a>忽略字符串大小写  
控制比较的区分大小写。  
  
-   如果你选择**True**，该比较将不区分大小写。  
  
-   如果你选择**False**，该比较将不区分大小写。  
  
### <a name="ignore-trailing-spaces"></a>忽略尾随空格  
控制如何尾随空格在比较过程中处理。  
  
-   如果你选择**True**，比较的字符串将右剪裁在进行比较前。  
  
-   如果你选择**False**，比较的字符串将保留尾随空格。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>指定过程和函数 （调用值） 的输入的的值  
你可以在指定输入的参数值**调用值**页。 **添加调用**按钮添加使用空的参数值的新调用。 **删除调用**按钮可移除当前的调用。  
  
## <a name="next-step"></a>下一步  
[选择并配置受影响的对象&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>另请参阅  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
