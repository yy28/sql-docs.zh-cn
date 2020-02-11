---
title: 指定表复制或查询（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 524e878933652699bef6e31da42d3a784b54df7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62892639"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>指定表复制或查询（SQL Server 导入和导出向导）
  使用 "**指定表复制或查询**" 页可以指定复制数据的方式。 您可以使用图形界面选择所希望复制的现有数据库对象，或使用 Transact-SQL 创建更复杂的查询。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **复制一个或多个表或视图中的数据**  
 使用 "**选择源表和视图**" 对话框将选定源表和视图中的字段复制到指定的目标。 如果希望在不对记录进行筛选或排序的情况下复制源中的所有数据，请使用此选项。  
  
 使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口连接到数据源时， **“复制一个或多个表或视图的数据”** 选项可能不可用。 此选项仅对在 ProviderDescriptors.xml 文件中有 ProviderDescription 部分的信息的那些访问接口可用。 每个 ProviderDescription 部分都包含从相应访问接口检索元数据所需的信息。 默认情况下，ProviderDescriptors.xml 文件仅包含以下访问接口的 ProviderDescription 部分：  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 若要使**一个或多个表或视图中的数据复制**选项可用于其他提供程序，第三方可以将其自己的 ProviderDescriptor 节添加到 providerdescriptors.xml 文件中。 默认情况下，此文件\<位于*驱动器*>： \Program Files\Microsoft SQL server\100\dts\providerdescriptors 若要查看 ProviderDescriptor 部分的要求，请参阅 ProviderDescriptors.xsd 架构文件，默认情况下，该文件位于 ProviderDescriptors.xml 文件所在的文件夹中。  
  
 **编写查询以指定要传输的数据**  
 使用 "**提供源查询**" 对话框生成用于检索行的 SQL 语句。 如果希望在复制操作中修改或限制源数据，请使用此选项。 只有符合选择条件的行才可用于复制。  
  
  
