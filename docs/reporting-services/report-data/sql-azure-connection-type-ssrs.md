---
title: "SQL Azure 连接类型 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 02/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c84def6c-e8cf-43d9-9912-098171a7ce79
caps.latest.revision: "17"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a3d5e93baee5b40bdbe4b27ac43103c9188fff7f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="sql-azure-connection-type-ssrs"></a>SQL Azure 连接类型 (SSRS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 是基于云的、构建在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术之上的托管关系数据库。 若要在报表中包括来自 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的数据，您必须有一个基于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]类型的报表数据源的数据集。 此内置数据源类型基于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据扩展插件。 使用此数据源类型可连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]并从中检索数据。  
  
 此数据扩展插件支持多值参数、服务器聚合以及与连接字符串分开管理的凭据。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 类似于内部部署的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，并且从 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中获取数据与从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中获取数据几乎是相同的（有少数例外）。  
  
> [!NOTE]  
>  打开到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的连接时，将连接超时值设置为 30 秒。  
  
 有关详细信息，请参阅 [docs.microsoft.com 上的 Microsoft Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/)。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]时，也会连接到云中的数据库对象。 正如现场数据库一样，托管数据库可能具有包含多个表、视图和存储过程的不同架构。 可在查询设计器中指定要使用的数据库对象。 如果未在连接字符串中指定数据库，则将连接到管理员为您分配的默认数据库。  
  
 请联系数据库管理员，获取连接信息以及用于连接到数据源的凭据。 下面的连接字符串示例指定一个名为 AdventureWorks 的托管示例数据库。  
  
```  
Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True;  
```  
  
 此外，使用 **“数据源属性”** 对话框还可以提供凭据，如用户名和密码。 `User Id` 和 `Password` 选项自动追加到连接字符串；您无需将它们作为连接字符串的一部分键入其中。  
  
 有关连接字符串示例的详细信息，请参阅 [报表生成器中的数据连接、数据源和连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
##  <a name="Credentials"></a> 凭据  
 不支持 Windows 身份验证（集成安全性）。 如果试图使用 Windows 身份验证连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，则会发生错误。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 仅支持 SQL Server 身份验证（用户名和密码），并且在每次连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]时，用户都必须提供凭据（登录名和密码）。  
  
 凭据必须具有足够的权限访问数据库。 根据要执行的查询，您可能需要具有其他权限，例如运行存储过程和访问表和视图的足够权限。 外部数据源的所有者必须配置相应的凭据，使这些凭据足以提供对所需数据库对象的只读访问。  
  
 在报表创作客户端，可以使用下列选项指定凭据：  
  
-   使用存储的用户名和密码。 若要协商当包含报表数据的数据库与报表服务器不同时产生的双跃点，请选择使用凭据作为 Windows 凭据的选项。 也可以选择在连接到数据源后模拟经过身份验证的用户。  
  
-   不需要提供任何凭据。 若要使用此选项，您必须具有为报表服务器配置的无人参与的执行帐户。 有关详细信息，请参阅 msdn.microsoft.com 上 [Reporting Services 文档](http://go.microsoft.com/fwlink/?linkid=121312)中的[配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 有关详细信息，请参阅[数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)或[在报表生成器中指定凭据](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Query"></a> 查询  
 查询指定了要为报表数据集检索哪些数据。 查询的结果集中的列填充数据集的字段集合。 如果查询返回多个结果集，则报表仅处理查询所检索的第一个结果集。 尽管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]之间存在一些差别（如所支持的数据库大小），但根据 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]编写查询类似于根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库编写查询。 有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（如 BACKUP）在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中不受支持，但在报表查询中是不会使用这些语句的。 有关详细信息，请参阅 [SQL Server 连接类型 (SSRS)](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)。  
  
 默认情况下，如果您创建一个新查询，或者打开一个可在图形查询设计器中显示的现有查询，则可以使用关系查询设计器。 可以通过下列方式指定查询：  
  
-   以交互方式生成查询。 使用关系查询设计器，此设计器显示表、视图、存储过程及其他数据库项按数据库架构组织的层次结构视图。 选择表或视图中的列，或者指定存储过程或表值函数。 通过指定筛选条件限制要检索的数据行数。 通过设置参数选项自定义报表运行时的筛选器。  
  
-   键入或粘贴查询。 使用基于文本的查询设计器直接输入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文本、粘贴来自其他来源的查询文本、输入使用关系查询设计器无法生成的复杂查询，或输入基于查询的表达式。  
  
-   从文件或报表中导入现有的查询。 使用任一查询设计器中的 **“导入查询”** 按钮浏览到 .sql 文件或 .rdl 文件，然后导入查询。  
  
 基于文本的查询设计器支持以下两种模式：  
  
-   [文本](#QueryText) 键入用于从数据源选择数据的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。  
  
-   [存储过程](#QueryStoredProcedure) 从存储过程的列表中进行选择。  
  
 有关详细信息，请参阅[关系查询设计器用户界面（报表生成器）](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md)和[基于文本的查询设计器用户界面（报表生成器）](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 使用的图形查询设计器提供对分组和聚合的内置支持，可帮助你编写仅检索摘要数据的查询。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语言功能包括：GROUP BY 子句、DISTINCT 关键字以及 SUM 和 COUNT 等聚合。 基于文本的查询设计器提供对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语言的完全支持，包括分组和聚合。 有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的详细信息，请参阅 msdn.microsoft.com 上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?LinkId=141687)中的 [Transact-SQL 引用（数据库引擎）](../../t-sql/transact-sql-reference-database-engine.md)。  
  
###  <a name="QueryText"></a> 使用 Text 查询类型  
 在基于文本的查询设计器中，可以键入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令来定义数据集中的数据。 例如，下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询选择职位为销售助理的所有雇员的姓名：  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 单击工具栏上的 **“运行”** 按钮 (**!**) 可以运行查询并显示结果集。  
  
 若要参数化此查询，请添加一个查询参数。 例如，将 WHERE 子句更改为下面的内容：  
  
```  
WHERE HumanResources.Employee.JobTitle = (@JobTitle)  
```  
  
 运行查询时，会自动创建与查询参数对应的报表参数。 有关详细信息，请参阅本主题后面的 [查询参数](#Parameters) 。  
  
  
###  <a name="QueryStoredProcedure"></a> 使用 StoredProcedure 查询类型  
 您可以采用以下方式之一为数据集查询指定存储过程：  
  
-   在 **“数据集属性”** 对话框中，设置 **“存储过程”** 选项。 从存储过程和表值函数的下拉列表中进行选择。  
  
-   在关系查询设计器中的“数据库视图”窗格中，选择存储过程或表值函数。  
  
-   在基于文本的查询设计器中，从工具栏中选择 **StoredProcedure** 。  
  
 选择存储过程或表值函数之后，就可以运行查询。 系统将提示您提供输入参数的值。 运行查询时，会自动创建与输入参数对应的报表参数。 有关详细信息，请参阅本主题后面的 [查询参数](#Parameters) 。  
  
 仅支持为存储过程检索到的第一个结果集。 如果存储过程返回多个结果集，则仅使用第一个结果集。  
  
 如果某个存储过程带有具有默认值的参数，则您可以访问该值，方法是使用 DEFAULT 关键字作为该参数的值。 如果该查询参数链接到某个报表参数，用户可以在报表参数的输入框中键入或选择单词 DEFAULT。  
  
 有关存储过程的详细信息，请参阅 msdn.microsoft.com 上 [SQL Server 联机丛书](http://go.microsoft.com/fwlink/?linkid=98335) 中的“存储过程（数据库引擎）”。  
  
  
##  <a name="Parameters"></a> Parameters  
 如果查询文本包含查询变量或具有输入参数的存储过程，则将自动生成数据集的对应查询参数和报表的报表参数。 查询文本不得包含针对每个查询变量的 DECLARE 语句。  
  
 例如，下面的 SQL 查询将创建一个名为 **EmpID**的报表参数：  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 默认情况下，各个报表参数的数据类型均为“Text”，并具有自动创建的数据集，以提供可用值的下拉列表。 创建报表参数后，您可能需要更改默认值。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)类型的报表数据源的数据集。  
  
  
##  <a name="Remarks"></a> 注释  
  
###### <a name="alternate-data-extensions"></a>备用数据扩展插件  
 您还可以通过使用 ODBC 数据源类型从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中检索数据。 不支持使用 OLE DB 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。  
  
 有关详细信息，请参阅 [ODBC 连接类型 (SSRS)](../../reporting-services/report-data/odbc-connection-type-ssrs.md)。  
  
###### <a name="platform-and-version-information"></a>平台和版本信息  
 有关平台和版本支持的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明。  
  
 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [向数据集添加筛选器（报表生成器和 SSRS）](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相关章节  
 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供访问报表数据的概述。  
  
 [报表生成器中的数据连接、数据源和连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供有关数据连接和数据源的信息。  
  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供有关嵌入数据集和共享数据集的信息。  
  
 [数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供有关查询生成的数据集字段集合的信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
  
## <a name="see-also"></a>另请参阅  
[docs.microsoft.com 上的 Microsoft Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/)  
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
 更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  
