---
title: "选择并配置的对象添加到测试 (SybaseToSQL) |Microsoft 文档"
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
helpviewer_keywords:
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e1cc9bf3ed4348e3875885c1c7bb6face6562753
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>选择并配置的对象添加到测试 (SybaseToSQL)
在此步骤中，您将选择对象进行测试，以及如何用于比较过程的和函数的输出参数，以及函数的返回值配置设置。  
  
## <a name="selection-of-objects-to-test"></a>选择向测试的对象  
在位于窗口左侧 Sybase 对象树中，检查你想要在测试过程中调用的对象。 请参阅中的可测试对象的完整列表[测试迁移的数据库对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)主题。  
  
如果 SSMA Tester 不支持任何选定的测试对象，你将看到该链接标记为**某些所选的对象包含错误**下对象树。 单击此链接来查看为什么是这些对象不能测试的原因并清除所选内容的错误的对象。  
  
在右侧，你可以查看多个页面**SQL**页显示当前对象的定义。 在**Pre SQL**和**Post SQL**页可以指定运行之前和之后的测试对象开始调用的脚本。 如果对象需要其他对象，此类的临时表或游标，这是可能很有用。 **参数**页列出了参数，如果对象是存储的过程或函数。 **属性**页显示的对象的其他特征。 请参阅说明**参数 Comparsions**和**调用值**下面的页面。  
  
## <a name="parameter-comparison-settings"></a>参数比较设置  
建立输出参数的比较规则和返回值中的**参数比较**页。 你可以进行以下设置。  
  
### <a name="use-during-comparisons"></a>在比较时使用  
启用使用的测试结果比较中的所选参数。  
  
-   如果你选择**True**，SSMA 上执行 Sybase 上具有相应的值的过程后将比较此参数的输出值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   如果你选择**False**，参数将从结果验证中排除。  
  
### <a name="use-custom-scale"></a>使用自定义比例  
近似和固定长度数值数据类型参数，可以设置自定义比例进行比较。  
  
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
[选择并配置受影响的对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[测试迁移数据库对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

