---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 013012ceb495ceb0b5b9e8fc207c9775713a8d5f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1803|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NO_SPACE|  
|消息正文|CREATE DATABASE 失败。 主文件必须至少是 %d MB 才能容纳模型数据库的副本。|  
  
## <a name="explanation"></a>解释  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过制作 model 数据库的副本来创建数据库。 然后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重命名该副本，并将新数据库放大到请求的大小。 此种情况下，用户尝试创建小于 model 数据库的数据库。 此操作失败了，其原因是主数据文件小于 model 数据库，无法容纳 model 数据库的副本。  
  
## <a name="user-action"></a>用户操作  
创建具有更大数据库文件大小的数据库。 如果希望收缩该数据库，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 DBCC SHRINKDATABASE 语句来执行此操作。  
  
