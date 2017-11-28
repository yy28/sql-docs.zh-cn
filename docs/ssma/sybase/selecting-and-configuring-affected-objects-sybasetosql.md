---
title: "选择并配置受影响的对象 (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 97bb6a73aa744a6471a48ba16fc3ee9b52dea67e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>选择并配置受影响的对象 (SybaseToSQL)
在此页中，你可以选择表和外键，在其中更改与其进行比较，如果 SSMA 验证上一步中选择的对象的执行结果。 此外，还可以自定义验证参数。  
  
## <a name="selection-of-affected-objects"></a>选择受影响的对象  
在位于窗口左侧 Sybase 对象树中，请检查表和外键，在其中更改应比较正在相同。  
  
如果 SSMA 测试人员无法验证任何这些对象，你将看到该链接标记为**某些所选的对象包含错误**下对象树。 单击此链接来查看为什么这些对象不能进行比较的原因并清除所选内容的错误的对象。  
  
## <a name="table"></a>表  
表选项卡包含选定的表的网格视图。 该网格包含有关所选表的以下信息：  
  
-   列名  
  
-   数据类型  
  
-   精度  
  
-   小数位数  
  
-   规则  
  
-   默认  
  
-   标识  
  
-   可以为 Null  
  
## <a name="sql"></a>Sql  
SQL 选项卡包含的"创建表"选定的表的 SQL。  
  
## <a name="data"></a>data  
数据选项卡显示所选表中显示的数据。  
  
## <a name="properties"></a>属性  
属性选项卡显示所选表的属性。 以下字段是属性选项卡下存在：  
  
-   创建或上次修改时间  
  
-   Object Name  
  
## <a name="table-comparison-settings"></a>表比较设置  
在建立表的比较规则**表比较**页。 你可以进行以下设置。  
  
### <a name="comparison-mode"></a>比较模式  
定义了表将执行比较。  
  
-   如果你选择**仅更改**，将执行的表行的完整比较。  
  
-   如果你选择**完整**，将执行的行所做的更改比较。  
  
## <a name="column-comparison-settings"></a>列比较设置  
建立在上表中的列的比较规则**列比较**页。 你可以进行以下设置。  
  
### <a name="use-during-test-comparisons"></a>在比较测试期间使用  
确定此列将参与测试结果验证。  
  
-   如果你选择**True**，SSMA 将 SQL Server 中的列的内容在 Sybase 上执行测试后比较此列的内容。
  
-   如果你选择**False**，将从结果验证中排除列。  
  
### <a name="use-custom-scale"></a>使用自定义比例  
对于数值数据类型的列，您可以设置比较自定义比例。  
  
-   如果你选择**True**，将根据舍入数字值**比较缩放**值之前对它们进行比较。  
  
-   如果你选择**False**，数值的比较将是准确。  
  
### <a name="comparing-scale"></a>比较缩放  
  
-   才可用**使用自定义比例**选项设置为**True**。 这是数值比较的精度。  
  
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
  
-   如果你选择**False**，比较将帐户的字母大小写。  
  
## <a name="comparing-sql"></a>比较 SQL  
你可以查看 SSMA tester 生成上的选择语句**比较 SQL**页。 测试人员将比较的结果集的行的行基于这些语句。 Sybase 结果集的每个下一行应该等于结果集生成中的下一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
你可以编辑这些 SELECT 语句，以提供自定义验证。 若要保存更改在 Sybase 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语句，使用**应用**相应按钮源和目标 SQL 下。  
  
## <a name="next-step"></a>下一步  
[自定义调用顺序 &#40;SybaseToSQL &#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[运行测试用例 &#40;SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[测试迁移数据库对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
