---
title: sysssispackagefolders (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7c1a5e117ee1c79b918f9785310b9b7c97671729
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025818"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个逻辑文件夹在文件夹层次结构中对应一行， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]使用。 在连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，将在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的对象资源管理器中列出这些文件夹。 文件夹会列出保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或文件系统中的包。  
  
 **Parentfolderid**列说明了在文件夹层次结构。 在文件夹层次结构顶部的文件夹包含中的 null 值**parentfolderid**。  
  
 **Foldername**列会包含在对象资源管理器中显示的文件夹的名称。  
  
 此表存储中**msdb**数据库。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|文件夹的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|父文件夹的 GUID。|  
|**foldername**|**sysname**|文件夹的名称。 该名称显示在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的文件夹层次结构中。|  
  
  
