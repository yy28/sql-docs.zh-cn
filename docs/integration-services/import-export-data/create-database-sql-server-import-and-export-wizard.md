---
title: 创建数据库（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4900f90f4044b32aea673106ad0a7a2a14a8f5cb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296289"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>创建数据库（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


如果在“选择目标”  页上选择“新建”  以创建新 SQL Server 目标数据库，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“创建数据库”  对话框。 在此页上，可以为新数据库提供名称。 （可选）还可以更改新数据库及其日志文件的初始大小和自动增长设置。 

向导中的“创建数据库”  对话框仅提供可用于创建新 SQL Server 数据库的基本选项。 若要查看和配置用于新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的所有选项，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建数据库或在向导创建数据库后对其进行配置。 

> [!NOTE]
> 如果在查找有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE DATABASE 语句的信息，而不是有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的“创建数据库”对话框的信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  

## <a name="screen-shot-of-the-create-database-page"></a>“创建数据库”页的屏幕截图  
以下屏幕截图显示向导的“创建数据库”  对话框。  

![导入和导出向导的创建数据库页](../../integration-services/import-export-data/media/create-database.png "导入和导出向导的创建数据库页")  

## <a name="provide-a-name-for-the-new-database"></a>提供新数据库的名称  
**名称**  
 为目标 SQL Server 数据库提供名称。
 
### <a name="naming-requirements"></a>命名要求
请确保对数据库命名时遵循 SQL Server 命名约定。  
  
-   数据库名称必须在 SQL Server 的实例内是唯一的。  
  
-   数据库名称最多可以包含 123 个字符。 （在最多 128 个字符中，这允许将 5 个字符用于 SQL Server 追加到数据文件和日志文件的后缀。）  
  
-   数据库名称必须符合 SQL Server 中的标识符规则。 以下是最重要的要求。  
  
    -   第一个字符必须是字母、下划线 (_)、at 符号 (@) 或数字符号 (#)。  
  
    -   后续字符可以是字母、数字、at 符号、美元符号 ($)、数字符号或下划线。  
  
    -   不能使用空格或其他特殊字符。  
  
有关这些要求的详细信息，请参阅 [数据库标识符](../../relational-databases/databases/database-identifiers.md)。  

## <a name="optionally-specify-data-file-and-log-file-options"></a>（可选）指定数据文件和日志文件选项

> [!TIP]
> 必须在“名称”  字段中为新数据库提供名称，但通常可以将用于文件大小和文件增长的其他设置保留为其默认值。

### <a name="data-file-options"></a>数据文件选项  
 **初始大小**  
 指定数据文件的初始大小 (MB)。  
  
 **不允许增长**  
 指示数据文件是否可以增长以超出指定的初始大小。  
  
 **增长百分比**  
 指定数据文件可以增长的百分比。  
  
 **增长规模**  
 指定数据文件可以增长的大小 (MB)。  
  
### <a name="log-file-options"></a>日志文件选项  
 **初始大小**  
 指定日志文件的初始大小 (MB)。  
  
 **不允许增长**  
 指示日志文件是否可以增长以超出指定的初始大小。  
  
 **增长百分比**  
 指定日志文件可以增长的百分比。  
  
 **增长规模**  
 指定日志文件可以增长的大小 (MB)。  

### <a name="more-info"></a>更多信息
有关在此页上看到的文件大小选项的详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 

## <a name="whats-next"></a>下一步是什么？  
 为向导将创建的新数据库提供名称并单击“确定”  之后，“创建数据库”  对话框会使你返回到“选择目标”  页。 有关详细信息，请参阅 [选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。  

