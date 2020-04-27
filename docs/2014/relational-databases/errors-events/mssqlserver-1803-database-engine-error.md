---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1fd65bf2c79c7360f2502975e911aea7ab225d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915260"
---
# <a name="mssqlserver_1803"></a>MSSQLSERVER_1803
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1803|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NO_SPACE|  
|消息正文|CREATE DATABASE 失败。 主文件必须至少是 %d MB 才能容纳模型数据库的副本。|  
  
## <a name="explanation"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过制作 model 数据库的副本来创建数据库。 然后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重命名该副本，并将新数据库放大到请求的大小。 此种情况下，用户尝试创建小于 model 数据库的数据库。 此操作失败了，其原因是主数据文件小于 model 数据库，无法容纳 model 数据库的副本。  
  
## <a name="user-action"></a>用户操作  
 创建具有更大数据库文件大小的数据库。 如果希望收缩该数据库，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 DBCC SHRINKDATABASE 语句来执行此操作。  
  
  
