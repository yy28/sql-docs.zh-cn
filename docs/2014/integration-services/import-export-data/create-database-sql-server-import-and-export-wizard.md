---
title: 创建数据库（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3720e3301eeffc73c8d89c901f2a4a337e1094d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099627"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>创建数据库（SQL Server 导入和导出向导）
  使用**Create Database**页后，可以定义为目标文件新的数据库。  
  
 此页提供了一部分可用于创建新数据库的选项。 若要查看所有选项，请使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解有关用于启动向导，选项以及已成功运行该向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为目标 SQL Server 数据库提供唯一的名称。 请确保对此数据库命名时遵循 SQL Server 约定。  
  
 **数据文件的名称**  
 查看数据文件的名称。 它是由以前提供的数据库名称派生而来的。  
  
 **日志文件名称**  
 查看日志文件的名称。 它是由以前提供的数据库名称派生而来的。  
  
 **初始大小 （数据文件）**  
 指定数据文件的初始大小 (MB)。  
  
 **不允许增长 （数据文件）**  
 指示数据文件是否可以增长以超出指定的初始大小。  
  
 **增长百分比 （数据文件）**  
 指定数据文件可以增长的百分比。  
  
 **增长规模 （数据文件）**  
 指定数据文件可以增长的大小 (MB)。  
  
 **初始大小 （日志文件）**  
 指定日志文件的初始大小 (MB)。  
  
 **不允许增长 （日志文件）**  
 指示日志文件是否可以增长以超出指定的初始大小。  
  
 **增长百分比 （日志文件）**  
 指定日志文件可以增长的百分比。  
  
 **增长规模 （日志文件）**  
 指定日志文件可以增长的大小 (MB)。  
  
  
