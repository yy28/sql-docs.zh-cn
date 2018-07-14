---
title: 引擎行为更改数据库的 SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- behavior changes [SQL Server]
- Database Engine [SQL Server], what's new
- Transact-SQL behavior changes
ms.assetid: 65eaafa1-9e06-4264-b547-cbee8013c995
caps.latest.revision: 134
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d83d502ec6b384a7c3e6a5f4ee2f4e7787ead4da
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193957"
---
# <a name="behavior-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 中数据库引擎功能的行为更改
  本主题介绍[!INCLUDE[ssDE](../includes/ssde-md.md)]中的行为更改。 与早期版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 相比， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的功能的工作或交互方式会受到行为更改的影响。  
  
## <a name="behavior-changes-in-includesssql14includessssql14-mdmd"></a>中的行为更改 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，如果对其运行查询的 XML 文档包含超过某一特定长度（超过 4020 个字符）的字符串，则查询可能会返回不正确的结果。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，此类查询将返回正确的结果。  
  
## <a name="behavior-changes-in-includesssql11includessssql11-mdmd"></a>中的行为更改 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="metadata-discovery"></a>元数据发现  
 中的改进[!INCLUDE[ssDE](../includes/ssde-md.md)]开头[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]允许 SQLDescribeCol 以获取更准确描述的预期的结果比在以前版本的返回 SQLDescribeCol [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../relational-databases/native-client/features/metadata-discovery.md)。  
  
 [SET FMTONLY](/sql/t-sql/statements/set-fmtonly-transact-sql)选项用于确定响应的格式，而不实际运行查询将被替换[sp_describe_first_result_set &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)， [sp_describe_undeclared_parameters &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql)， [sys.dm_exec_describe_first_result_set &#40;-&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql)，和[sys.dm_exec_describe_first_result_set_for_object &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql)。  
  
### <a name="changes-to-behavior-in-scripting-a-sql-server-agent-task"></a>有关为 SQL Server 代理任务编写脚本的行为的更改  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，如果您通过复制现有作业中的脚本来创建新作业，则新作业可能会无意中影响现有作业。 若要创建新的作业使用现有作业中的脚本，请手动删除参数*@schedule_uid*通常是最后一个参数的部分中的现有作业中创建作业计划。 这将为新作业创建新的独立计划而不影响现有作业。  
  
### <a name="constant-folding-for-clr-user-defined-functions-and-methods"></a>CLR 用户定义函数和方法的常量折叠  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，以下用户定义的 CLR 对象现已可折叠：  
  
-   确定性的标量值 CLR 用户定义函数。  
  
-   确定性的 CLR 用户定义类型的方法。  
  
 此改进旨在增强当使用相同的参数多次调用这些函数或方法时的性能。 但是，此更改可能会在非确定性函数或方法被错误标记为确定性函数或方法时导致意外结果。 CLR 函数或方法的确定性由 `IsDeterministic` 或 `SqlFunctionAttribute` 的 `SqlMethodAttribute` 属性的值指示。  
  
### <a name="behavior-of-stenvelope-method-has-changed-with-empty-spatial-types"></a>具有空的空间类型的 STEnvelope() 方法的行为已更改  
 具有空对象的 `STEnvelope` 方法的行为现在与其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 空间方法的行为保持一致。  
  
 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，在使用空对象调用 `STEnvelope` 方法时，该方法返回以下结果：  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns POINT EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns LINESTRING EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns POLYGON EMPTY  
```  
  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，现在使用空对象调用 `STEnvelope` 方法时，该方法返回以下结果：  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
```  
  
 若要确定空间对象是否为空，请调用[STIsEmpty &#40;geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type)方法。  
  
### <a name="log-function-has-new-optional-parameter"></a>LOG 函数具有新的可选参数  
 `LOG`函数现在具有一个可选*基*参数。 有关详细信息，请参阅[日志&#40;TRANSACT-SQL&#41;](/sql/t-sql/functions/log-transact-sql)。  
  
### <a name="statistics-computation-during-partitioned-index-operations-has-changed"></a>已分区索引操作期间的统计信息计算已更改  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，当创建或重新生成已分区索引时，并非通过扫描表中的所有行来创建统计信息。 相反，查询优化器使用默认采样算法来生成统计信息。 在升级具有已分区索引的数据库后，您可以在直方图数据中注意到针对这些索引的差异。 此行为更改可能不会影响查询性能。 若要通过扫描表中所有行的方法获得有关已分区索引的统计信息，请使用 CREATE STATISTICS 或 UPDATE STATISTICS 以及 FULLSCAN 子句。  
  
### <a name="data-type-conversion-by-the-xml-value-method-has-changed"></a>通过 XML value 方法进行的数据类型转换已更改  
 `value` 数据类型的 `xml` 方法的内部行为已更改。 此方法对 XML 执行 XQuery，并返回指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据类型的标量值。 xs 类型必须转换为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据类型。 以前，`value` 方法在内部将源值转换为 xs:string，然后将 xs:string 转换为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据类型。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，以下情况下将跳过到 xs:string 的转换：  
  
|源 XS 数据类型|目标 SQL Server 数据类型|  
|-------------------------|--------------------------------------|  
|byte<br /><br /> short<br /><br /> ssNoversion<br /><br /> integer<br /><br /> long<br /><br /> unsignedByte<br /><br /> unsignedShort<br /><br /> unsignedInt<br /><br /> unsignedLong<br /><br /> positiveInteger<br /><br /> nonPositiveInteger<br /><br /> negativeInteger<br /><br /> nonNegativeInteger|TINYINT<br /><br /> SMALLINT<br /><br /> ssNoversion<br /><br /> BIGINT<br /><br /> Decimal<br /><br /> NUMERIC|  
|Decimal|Decimal<br /><br /> NUMERIC|  
|FLOAT|REAL|  
|double|FLOAT|  
  
 新行为改进了可跳过中间转换时的性能。 但是，当数据类型转换失败时，您看到的错误消息将有别于从中间 xs:string 值进行转换时引发的错误消息。 例如，如果 value 方法未能将 `int` 值 100000 转换为 `smallint`，则之前的错误消息为：  
  
 `The conversion of the nvarchar value '100000' overflowed an INT2 column. Use a larger integer column.`  
  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，如果没有到 xs:string 的中间转换，则错误消息为：  
  
 `Arithmetic overflow error converting expression to data type smallint.`  
  
### <a name="sqlcmdexe-behavior-change-in-xml-mode"></a>XML 模式中的 sqlcmd.exe 行为更改  
 如果在执行 SELECT * from T FOR XML … 时通过 XML 模式（:XML ON 命令）使用 sqlcmd.exe，则会出现行为更改。  
  
### <a name="dbcc-checkident-revised-message"></a>DBCC CHECKIDENT 修改了消息  
 在中[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]，由 DBCC CHECKIDENT 命令返回的消息已更改仅当它用于重新设定种子*new_reseed_value*若要更改当前标识值。 新的消息是"正在检查标识信息： 当前标识值 '\<当前标识值 >。 DBCC 执行完毕。 如果 DBCC 输出了错误消息，请与系统管理员联系。”  
  
 在早期版本中，消息是"正在检查标识信息： 当前标识值\<当前标识值 >'，当前列值 '\<当前列的值 >。 DBCC 执行完毕。 如果 DBCC 输出了错误消息，请与系统管理员联系。” 在使用 NORESEED 指定 DBCC CHECKIDENT 时（没有第二个参数或没有重设种子值），该消息保持不变。 有关详细信息，请参阅 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)。  
  
### <a name="behavior-of-exist-function-on-xml-datatype-has-changed"></a>XML 数据类型的 exist() 函数的行为已更改  
 行为**exist （)** 比较 XML 数据类型为 0 （零） 值为 null 时，函数已更改。 请参考如下示例：  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 0;  
```  
  
 在早期版本中，此比较将返回 1 (true)；现在，此比较将返回 0（零，false）。  
  
 以下比较未发生更改：  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 1; -- 0 expected, 0 returned  
SELECT COUNT(1) WHERE @test.exist('/dogs') IS NULL; -- 1 expected, 1 returned  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中数据库引擎功能的重大更改](breaking-changes-to-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中弃用的数据库引擎功能](deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中废止的数据库引擎功能](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
