---
title: sysssispackagefolders （Transact-sql） |Microsoft Docs
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
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 67ab7ee0d6d4be6986022d4ee470f19adffce65c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633435"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  使用的文件夹层次结构中的每个逻辑文件夹在列中占一行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。 在连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，将在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的对象资源管理器中列出这些文件夹。 文件夹会列出保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或文件系统中的包。  
  
 **Parentfolderid**列描述文件夹层次结构。 位于文件夹层次结构顶部的文件夹在**parentfolderid**中包含 null 值。  
  
 "**文件夹**名称" 列包含在对象资源管理器中显示的文件夹的名称。  
  
 该表存储在**msdb**数据库中。  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|文件夹的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|父文件夹的 GUID。|  
|**名**|**sysname**|文件夹的名称。 该名称显示在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的文件夹层次结构中。|  
  
  
