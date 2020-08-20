---
description: Integration Services 表 (Transact-SQL)
title: " (Transact-sql) Integration Services 表 |Microsoft Docs"
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 05f7e319dbaec37761eb5488f9d9a33cce09f3a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473239"
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services 表 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本节中的主题介绍 msdb 数据库中存储所用信息的系统表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
## <a name="in-this-section"></a>本节内容  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包在运行时生成的每个日志条目在表中各占一行。  
  
 仅当包使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志提供程序时，才会使用此表。  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务用于组织包的每个逻辑文件夹在表中各占一行。 列值定义嵌套文件夹之间的父/子关系。  
  
> [!NOTE]  
>  当连接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 服务时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 以层次结构视图显示存储的包。  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 每个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包在表中各占一行。  
  
 仅当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中存储包时，才会使用此表。  
  
  
