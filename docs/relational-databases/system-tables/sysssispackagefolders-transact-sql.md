---
title: sysssispackagefolders (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
caps.latest.revision: ''
author: douglasl
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c623e7e486022804b8b9722c1ec5201dd64c8a1
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个文件夹层次结构中的逻辑文件夹中对应一行， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]使用。 在连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，将在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的对象资源管理器中列出这些文件夹。 文件夹会列出保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或文件系统中的包。  
  
 **Parentfolderid**列描述文件夹层次结构。 在文件夹层次结构顶部的文件夹包含中的 null 值**parentfolderid**。  
  
 **Foldername**列包含在对象资源管理器中显示的文件夹的名称。  
  
 此表存储在**msdb**数据库。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|文件夹的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|父文件夹的 GUID。|  
|**foldername**|**sysname**|文件夹的名称。 该名称显示在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的文件夹层次结构中。|  
  
  
