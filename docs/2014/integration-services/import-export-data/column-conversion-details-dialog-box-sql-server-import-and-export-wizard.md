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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9207e76191060c56acad37db734827579a83aae0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436824"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>“列转换详细信息”对话框（SQL Server 导入和导出向导）
  使用 "**列转换详细信息**" 对话框可以查看有关单个列的详细转换信息。 此转换信息包含源和目标中的列的数据类型以及向导将执行的转换。 此页还列出了向导用于确定所需的数据类型转换的数据类型映射文件。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在安装过程中会安装这些数据类型映射文件。  
  
 **打开“列转换详细信息”对话框**  
  
1.  在导入和导出向导的 "**查看数据类型问题**" 页上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 "**表**" 列表中，选择一个表。  
  
2.  在 "**数据类型映射**" 列表中，双击包含要查看其转换详细信息的列的行。  
  
 若要了解有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
  
