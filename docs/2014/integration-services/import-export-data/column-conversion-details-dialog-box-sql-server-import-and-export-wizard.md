---
title: “列转换详细信息”对话框（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd7abb585c8f6a44fa8a3e107146e7f74dcbb11c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821954"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>“列转换详细信息”对话框（SQL Server 导入和导出向导）
  使用**列转换详细信息**对话框可以查看有关单个列的详细的转换信息。 此转换信息包含源和目标中的列的数据类型以及向导将执行的转换。 此页还列出了向导用于确定所需的数据类型转换的数据类型映射文件。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在安装过程中会安装这些数据类型映射文件。  
  
 **若要打开列转换详细信息对话框**  
  
1.  上**查看数据类型问题**页[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导中，在**表**列表中，选择一个表。  
  
2.  在中**数据类型映射**列表中，双击包含您要查看转换详细信息的列的行。  
  
 若要详细了解[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解有关用于启动向导，选项以及已成功运行该向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
  
