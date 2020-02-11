---
title: Create Table SQL 语句（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f541ad24e87bf5bdea9ed8b8c2523a73c81daa9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767999"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>Create Table SQL 语句（SQL Server 导入和导出向导）
  使用 "**创建表 SQL 语句**" 对话框可以查看自动生成的语句，或根据需要修改该语句。 如果修改此语句，可能还必须对列映射做相关联的更改，而且此后必须手动维护编辑过的 SQL 语句。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将基于连接数据源生成一个默认的 CREATE TABLE 语句。 即使源表包含一个已声明了 FILESTREAM 属性的列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。 若要运行具有 FILESTREAM 属性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，首先要在目标数据库上实现 FILESTREAM 存储。 然后在 **“创建表”** 对话框中将 FILESTREAM 属性添加到 CREATE TABLE 语句中。 有关详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **SQL 语句**  
 显示自动生成的 SQL 语句，允许对其进行编辑。  
  
> [!NOTE]  
>  如果要在 SQL 语句中包括回车符，请按 Ctrl+Enter。 如果只按 Enter，则对话框将关闭。  
  
 **自动生成**  
 如果已修改了 SQL 语句，通过单击“自动生成”**** 可以还原默认的 SQL 语句。  
  
  
