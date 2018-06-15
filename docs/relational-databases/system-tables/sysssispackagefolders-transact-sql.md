---
title: sysssispackagefolders (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
caps.latest.revision: 22
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fb24e752bf92704b1560aa84906f28173a0d9dc0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258248"
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
|**文件夹名称**|**sysname**|文件夹的名称。 该名称显示在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的文件夹层次结构中。|  
  
  
