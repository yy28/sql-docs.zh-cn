---
title: 选择并配置受影响的对象 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: c06fb621cab581e934ba4655ed6507149d109c60
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266497"
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>选择并配置受影响的对象 (OracleToSQL)
在此页可以选择表和外键，在其中更改应进行比较时 SSMA 验证在上一步中选择的对象的执行结果。 此外，还可以自定义验证参数。  
  
## <a name="selection-of-affected-objects"></a>选择的受影响的对象  
在位于左侧和右侧的窗口上 Oracle 对象树中，检查表和外键，在其中更改应进行比较以相同。  
  
SSMA 测试人员无法验证任何这些对象，如果你将看到标记为链接**有些选定的对象包含错误**在对象树。 单击此链接可查看这些对象为何不能进行比较的原因，从而清除所选的错误的对象。  
  
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
SQL 选项卡包含"创建表"选定的表的 SQL。  
  
## <a name="data"></a>Data  
数据选项卡显示所选择的表中的数据。  
  
## <a name="properties"></a>properties  
属性选项卡显示所选表的属性。 以下字段是属性选项卡下存在：  
  
-   创建或上次修改时间  
  
-   Object Name  
  
## <a name="columns-comparison-settings"></a>列比较设置  
建立在上表中的列的比较规则**列比较**页。 可以进行以下设置。  
  
### <a name="use-during-test-comparisons"></a>比较测试期间使用  
确定此列将参与测试结果验证。  
  
-   如果愿意 **，则返回 True**，SSMA 在 Oracle 上执行测试，并显示在 SQL Server 中列的内容后将比较此列的内容。 
  
-   如果愿意**False**，将从结果验证中排除列。  
  
### <a name="use-custom-scale"></a>使用自定义缩放  
对于数值数据类型的列，可以设置用于比较的自定义规模。  
  
-   如果愿意 **，则返回 True**，将根据舍入数字值**比较规模**值之前对它们进行比较。  
  
-   如果愿意**False**，数值比较将是准确。  
  
### <a name="comparing-scale"></a>比较规模  
  
-   才可用**使用自定义比例**选项设置为**True**。 这是数值比较的精度。  
  
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
  
-   如果愿意**False**，比较将考虑字母大小写。  
  
## <a name="comparing-sql"></a>比较 SQL  
您可以查看在生成的 SSMA 测试人员的选择语句**比较 SQL**页。 测试人员将比较行的行按这些语句的结果集。 Oracle 结果集的每个下一步行应等于下一行的 SQL Server 中生成的结果集。
  
您可以编辑这些 SELECT 语句，以提供自定义验证。 若要保存所做的更改，在 Oracle 中也可以在 SQL Server 语句，请使用**应用**按钮下的源和目标 SQL，相应地。  
  
## <a name="next-step"></a>下一步  
[自定义调用顺序&#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[完成测试用例准备&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[运行测试用例&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[测试迁移的数据库对象&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
