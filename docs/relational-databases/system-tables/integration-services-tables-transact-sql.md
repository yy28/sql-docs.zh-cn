---
title: Integration Services 表 (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
caps.latest.revision: 21
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc5df46211b3de92b054fea4120d9b7c884a0ccb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259617"
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services 表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本部分中的主题说明 msdb 数据库中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 用于存储信息的系统表。  
  
## <a name="in-this-section"></a>本節內容  
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
  
  
