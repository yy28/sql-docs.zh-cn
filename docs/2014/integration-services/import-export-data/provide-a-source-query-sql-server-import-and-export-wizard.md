---
title: 提供源查询（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7a028c880d87e21e1fcc63ffc605e7d375619dbf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767859"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>提供源查询（SQL Server 导入和导出向导）
  使用 "**提供源查询**" 页可以键入将生成要从数据源复制到目标的数据的 SQL 语句。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **SQL 语句**  
 键入查询语句，以便从源数据库中检索所选的数据行。 例如，以下查询语句可以从 AdventureWorks 数据库中检索提成比例超过 1.5% 的销售人员的 **SalesPersonID**、 **SalesQuota**和 **SalesYTD** 。  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **分析**  
 检查“SQL 语句”**** 文本框中 SQL 语句的语法。  
  
> [!NOTE]  
>  如果检查语句的语法所需的时间超过超时值（30 秒），则将停止分析并生成错误。 在成功完成分析之前，您将无法跳过向导的这一页。 一种解决方案是基于查询创建数据库视图，然后从向导查询该视图，而不是直接输入查询文本。  
  
 **“浏览”**  
 使用 "**打开**" 对话框选择包含 SQL 语句的文件。 选择一个文件可以将该文件中的文本复制到 **“查询语句”** 文本框中。  
  
  
