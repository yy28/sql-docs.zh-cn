---
title: SQL Server 连接类型 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 957e7091-e08f-48d2-9506-872227ae8b20
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 30af34c41cbea7d28e78d2684ce2aa316b116b39
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196977"
---
# <a name="sql-server-connection-type-ssrs"></a>SQL Server 连接类型 (SSRS)
  若要在报表中包括来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的数据，您必须具有一个基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型的报表数据源的数据集。 此内置数据源类型基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据扩展插件。 使用此数据源类型可连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的当前版本和早期版本并从中检索数据。  
  
 此数据扩展插件支持多值参数、服务器聚合以及与连接字符串分开管理的凭据。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅[添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 当连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库时，您将会连接到服务器上一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的数据库对象。 该数据库可能具有包含多个表、视图和存储过程的不同架构。 可在查询设计器中指定要使用的数据库对象。 如果未在连接字符串中指定数据库，则将连接到数据库管理员为您分配的默认数据库。  
  
 请联系数据库管理员，获取连接信息以及用于连接到数据源的凭据。 下面的连接字符串示例指定本地客户端上的示例数据库：  
  
```  
Data Source=<server>;Initial Catalog=AdventureWorks  
```  
  
 有关连接字符串示例的详细信息，请参阅 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 在报表创作客户端，可以使用下列选项指定凭据：  
  
-   当前 Windows 用户（也称为集成安全性）。  
  
-   使用存储的用户名和密码。  
  
-   提示用户输入凭据。 此选项仅支持 Windows 集成安全性。  
  
-   不需要提供任何凭据。 若要使用此选项，您必须具有为报表服务器配置的无人参与的执行帐户。 有关详细信息，请参阅 msdn.microsoft.com 上 [Reporting Services 文档](http://go.microsoft.com/fwlink/?linkid=121312)中的[配置无人参与的执行帐户（SSRS 配置管理器）](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 有关详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或[在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
  
##  <a name="Query"></a> 查询  
 查询指定了要为报表数据集检索哪些数据。 查询的结果集中的列填充数据集的字段集合。 报表仅处理查询检索的第一个结果集。  
  
 默认情况下，如果您创建一个新查询，或者打开一个可在图形查询设计器中显示的现有查询，则可以使用关系查询设计器。 可以通过下列方式指定查询：  
  
-   以交互方式生成查询。 使用关系查询设计器，此设计器显示表、视图、存储过程及其他数据库项按数据库架构组织的层次结构视图。 选择表或视图中的列，或者指定存储过程或表值函数。 通过指定筛选条件限制要检索的数据行数。 通过设置参数选项自定义报表运行时的筛选器。  
  
-   键入或粘贴查询。 使用基于文本的查询设计器直接输入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文本、粘贴来自其他来源的查询文本、输入使用关系查询设计器无法生成的复杂查询，或输入基于查询的表达式。  
  
-   从文件或报表中导入现有的查询。 使用任一查询设计器中的 **“导入查询”** 按钮浏览到 .sql 文件或 .rdl 文件，然后导入查询。  
  
 有关详细信息，请参阅[关系查询设计器用户界面（报表生成器）](relational-query-designer-user-interface-report-builder.md)和[基于文本的查询设计器用户界面（报表生成器）](text-based-query-designer-user-interface-report-builder.md)。  
  
 支持以下查询模式：  
  
-   [文本](#QueryText) 键入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。  
  
-   [存储过程](#QueryStoredProcedure) 从存储过程的列表中进行选择。  
  
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
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 运行查询时，会自动创建与查询参数对应的报表参数。 有关详细信息，请参阅本主题后面的 [查询参数](#Parameters) 。  
  
  
###  <a name="QueryStoredProcedure"></a> 使用 StoredProcedure 查询类型  
 您可以采用以下方式之一为数据集查询指定存储过程：  
  
-   在 **“数据集属性”** 对话框中，设置 **“存储过程”** 选项。 从存储过程和表值函数的下拉列表中进行选择。  
  
-   在关系查询设计器中的“数据库视图”窗格中，选择存储过程或表值函数。  
  
-   在基于文本的查询设计器中，从工具栏中选择 **StoredProcedure** 。  
  
 选择存储过程或表值函数之后，就可以运行查询。 系统将提示您提供输入参数的值。 运行查询时，会自动创建与输入参数对应的报表参数。 有关详细信息，请参阅本主题后面的 [查询参数](#Parameters) 。  
  
 仅支持为存储过程检索到的第一个结果集。 如果存储过程返回多个结果集，则仅使用第一个结果集。  
  
 如果某个存储过程带有具有默认值的参数，则您可以访问该值，方法是使用 DEFAULT 关键字作为该参数的值。 如果该查询参数链接到某个报表参数，用户可以在报表参数的输入框中键入或选择单词 DEFAULT。  
  
 有关详细信息，请参阅 msdn.microsoft.com 上 [SQL Server 联机丛书](http://go.microsoft.com/fwlink/?linkid=98335) 中的“存储过程（数据库引擎）”。  
  
  
##  <a name="Parameters"></a> Parameters  
 如果查询文本包含查询变量或具有输入参数的存储过程，则将自动生成数据集的对应查询参数和报表的报表参数。 查询文本不得包含针对每个查询变量的 DECLARE 语句。  
  
 例如，下面的 SQL 查询将创建一个名为 `EmpID` 的报表参数：  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 报表参数是用可能需要修改的默认属性值创建的。 例如：  
  
-   默认情况下，每个报表参数的数据类型均为 **Text**。 如果基础数据属于其他数据类型，则必须更改参数的数据类型。  
  
-   如果选择多值参数选项，则必须手动更改查询以测试值是否属于集的使用`IN`运算符，例如， `WHERE EmployeeID IN (@EmpID)`。  
  
 有关详细信息，请参阅[报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)。  
  
  
##  <a name="Remarks"></a> 注释  
 您还可以通过使用 OLE DB 或 ODBC 数据源类型从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中检索数据。 有关详细信息，请参阅 [OLE DB 连接类型 (SSRS)](ole-db-connection-type-ssrs.md) 或 [ODBC 连接类型 (SSRS)](odbc-connection-type-ssrs.md)。  
  
###### <a name="platform-and-version-information"></a>平台和版本信息  
 有关平台和版本支持的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明。  
  
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [向数据集添加筛选器（报表生成器和 SSRS）](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相关章节  
 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)  
 提供访问报表数据的概述。  
  
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 提供有关数据连接和数据源的信息。  
  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供有关嵌入数据集和共享数据集的信息。  
  
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)  
 提供有关查询生成的数据集字段集合的信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
  
## <a name="see-also"></a>请参阅  
 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
