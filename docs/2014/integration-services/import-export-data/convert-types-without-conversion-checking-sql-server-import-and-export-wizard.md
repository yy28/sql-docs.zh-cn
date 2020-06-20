---
title: 转换类型时不进行转换检查（SQL Server 导入和导出向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.nomappingfile.f1
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f06e60f052dad10b0e69ef0aa6a879e3d29d1f86
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965627"
---
# <a name="convert-types-without-conversion-checking-sql-server-import-and-export-wizard"></a>转换类型时不进行转换检查（SQL Server 导入和导出向导）
  如果向导找不到一个或多个数据类型转换和映射文件，则使用 "**转换类型而不进行转换检查**" 页可以查看向导执行的映射 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。 此页包含的信息可帮助您识别缺少的文件。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
  
