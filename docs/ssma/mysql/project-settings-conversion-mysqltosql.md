---
title: "项目设置 （转换） (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
caps.latest.revision: "19"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9062c61ad2a799a20370c8b406843e0e4a209869
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-conversion-mysqltosql"></a>项目设置 （转换） (MySQLToSQL)
转换页**项目设置**对话框中包含自定义如何 SSMA 将 MySQL 语法转换为 SQL Server 或 SQL Azure 语法的设置。  
  
转换窗格位于**项目设置**和**默认项目设置**对话框。  
  
-   使用**默认项目设置**对话框中设置的所有项目的配置选项。 若要访问的转换设置中，在**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看 / 更改，不再是迁移项目类型**迁移目标版本**下拉列表中，单击**常规**底部的左窗格中，，然后选择**转换**。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**常规**中左窗格中，然后单击底部**转换**。  
  
## <a name="options"></a>“常规”  
  
### <a name="collate-clause"></a>Collate 子句  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**COLLATE 子句的显式转换**|显式 COLLATE 子句转换选项指定如何将转换 MySQL 代码中的显式 COLLATE 子句。 可能的选项： 忽略，但出现警告标记/生成错误<br /><br />**默认模式**： 忽略和警告标记<br /><br />**开放式模式**： 忽略和警告标记<br /><br />**完整模式**： 忽略和警告标记|  
  
### <a name="column-constraints"></a>列约束  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**为枚举数据类型的列生成约束**|如果不存在的 MySQL 表中，将在 SQL Server 或 SQL Azure 表中，生成枚举数据类型的列的约束。 如果是，枚举数据类型的所有转换后的列将伴随控制值的 CHECK 约束。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
|**为组数据类型的列生成约束**|如果不存在的 MySQL 表中，请在 SQL Server 或 SQL Azure 表中，生成一组数据类型的列的约束。 如果是，都将转换后的所有列，将数据类型设置的都伴随具有控制值的 CHECK 约束。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
|**为无符号的数值数据类型列的列生成约束**|将非负值检查添加到无符号的数值数据类型的列中。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
|**为每年的数据类型列生成约束**|如果不存在的 MySQL 表中，将在 SQL Server 或 SQL Azure 表中，生成年的数据类型列的约束。 如果是，所有转换后的列的年数据类型将带有具有控制值的 CHECK 约束。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
  
### <a name="data-types"></a>数据类型  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**枚举数据类型转换**|指定作为转换为 NVARCHAR 或转换为数字应当如何转换 MySQL 枚举数据类型<br /><br />**默认模式**： 将转换为 NVARCHAR<br /><br />**开放式模式**： 将转换为 NVARCHAR<br /><br />**完整模式**： 将转换为 NVARCHAR|  
|**组的数据类型转换**|指定如何应为 MySQL 设置数据类型转换，转换为 NVARCHAR (L) 将转换为 BINARY(L) /<br /><br />**默认模式**： 将转换为 NVARCHAR(L)<br /><br />**开放式模式**： 将转换为 NVARCHAR(L)<br /><br />**完整模式**： 将转换为 NVARCHAR(L)|  
  
### <a name="generic"></a>泛型  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**无中插入和替换默认值的列**|如果是，引用表使用 MyISAM 和 InnoDb 以外的存储的引擎的所有语句应都标记为警告转换消息。<br /><br />**默认模式**： 将添加到列列表<br /><br />**开放式模式**： 将添加到列列表<br /><br />**完整模式**： 将添加到列列表|  
|**除数为零转换生成**|指定没有任何 ERROR_FOR_DIVISION_BY_ZERO 行为模拟 MySQL。<br /><br />**默认模式**： 错误<br /><br />**开放式模式**： 错误<br /><br />**完整模式**: NULL|  
|**IN 运算符**|指定如何将转换 MySQL IN 运算符。<br /><br />**默认模式**： 始终将转换为在<br /><br />**开放式模式**： 始终将转换为在<br /><br />**完整模式**： 根据需要展开|  
|**MySQL 函数转换**|指定如何将 MySQL 标准函数转换。<br /><br />**默认模式**： 乐观<br /><br />**开放式模式**： 乐观<br /><br />**完整模式**： 精确|  
|**不支持存储引擎**|如果是，引用表使用 MyISAM 和 InnoDb 以外的存储的引擎的所有语句应都标记为警告转换消息。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
|**禁止 ROWID 辅助列生成**|如果是，禁止 ROWD 辅助列创建目标表上创建。 可能会影响某些结构的迁移。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**： 否|  
|**TRUNCATE 语句转换**|指定如何将转换截断语句。<br /><br />**默认模式**： 截断<br /><br />**开放式模式**： 截断<br /><br />**完整模式**： 截断|  
  
### <a name="misc"></a>杂项  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**默认架构映射**|指定如何将 MySQL 数据库映射到 SQL Server 架构。<br /><br />**默认模式**： 数据库到数据库<br /><br />**开放式模式**： 数据库到数据库<br /><br />**完整模式**： 数据库到数据库|  
  
### <a name="procedures-and-functions"></a>过程和功能  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**默认函数转换**|指定是否函数都将默认情况下会转换到 T-SQL 的函数或存储过程。<br /><br />**默认模式**： 将转换为函数<br /><br />**开放式模式**： 将转换为函数<br /><br />**完整模式**： 将转换为函数|  
|**在生成集 XACT_ABORT**|指定需要添加到转换后的过程或触发器的开头 SET XACT_ABORT ON。<br /><br />**默认模式**: 是<br /><br />**开放式模式**: 是<br /><br />**完整模式**: 是|  
|**在生成集 NOCOUNT**|指定需要添加到转换后的过程或触发器的开头 SET NOCOUNT ON。<br /><br />**默认模式**: 是<br /><br />**开放式模式**: 是<br /><br />**完整模式**: 是|  
  
### <a name="spatial-data-types"></a>空间数据类型  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**默认 {XMAX &#124; 边界框XMIN &#124;YMAX &#124;YMIN} 用于空间索引**|定义默认值为 {XMAX &#124;XMIN &#124;YMAX &#124;边界框用于空间索引 YMIN} 参数。<br /><br />**默认模式**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**开放式模式**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**完整模式**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**空间索引的默认网格密度**|定义 LEVEL_1、 LEVEL_2、 LEVEL_3 和用于空间索引的网格密度 LEVEL_4 的默认值。<br /><br />**默认模式**<br /><br />LEVEL_1： 默认<br /><br />LEVEL_2： 默认<br /><br />LEVEL_3： 默认<br /><br />LEVEL_4： 默认<br /><br />**开放式模式**<br /><br />LEVEL_1： 默认<br /><br />LEVEL_2： 默认<br /><br />LEVEL_3： 默认<br /><br />LEVEL_4： 默认<br /><br />**完整模式**<br /><br />LEVEL_1： 默认<br /><br />LEVEL_2： 默认<br /><br />LEVEL_3： 默认<br /><br />LEVEL_4： 默认|  
  
### <a name="transactions"></a>中的  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**非事务性表**|指定对表不支持事务的所有引用应都标记为警告转换消息。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
|**事务隔离级别**|指定事务隔离级别应使用的新事务。<br /><br />**默认模式**： 默认<br /><br />**开放式模式**： 默认<br /><br />**完整模式**: Repeatable read|  
  
### <a name="value-control"></a>值控件  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**到数值转换的字符**|指定如何处理隐式和显式从字符数据类型转换为数值数据类型。<br /><br />**默认模式**： 乐观<br /><br />**开放式模式**： 乐观<br /><br />**完整模式**： 精确|  
|**控制无符号的数字值**|将值分配到无符号的数值变量和参数的控件。<br /><br />**默认模式**： 否<br /><br />**开放式模式**： 否<br /><br />**完整模式**: 是|  
|**控件的无符号的减法**|修改插入到无符号数据类型的表列的负值。<br /><br />**默认模式**： 转换作为-是 '<br /><br />**开放式模式**： 转换作为-是 '<br /><br />**完整模式**： 带有警告标记|  
|**转换到和从二进制数据类型**|指定如何处理从二进制数据类型的隐式和显式转换。<br /><br />**默认模式**： 乐观<br /><br />**开放式模式**： 乐观<br /><br />**完整模式**： 精确|  
|**转换为日期/时间数据类型**|指定如何处理隐式和显式转换为日期/时间数据类型。<br /><br />**默认模式**： 模拟 MySQL 格式<br /><br />**开放式模式**： 使用 SQL Server 格式<br /><br />**完整模式**： 模拟 MySQL 格式|  
|**数值精度超出 38**|指定如何将数值转换超过 38 的精度。<br /><br />**默认模式**： 如有可能舍入<br /><br />**开放式模式**： 如有可能舍入<br /><br />**完整模式**： 如有可能舍入|  
|**NOT NULL 列中的零日期**|指定如何处理分配给 NOT NULL 列的零日期，零中日期值或无效的日期/时间值。<br /><br />**默认模式**: getdate （） 函数<br /><br />**开放式模式**: getdate （） 函数<br /><br />**完整模式**: getdate （） 函数|  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考 &#40;MySQLToSQL &#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
