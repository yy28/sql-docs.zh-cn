---
title: MSSQLSERVER_21862 | Microsoft Docs
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
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea459faf94613bc26a99192762fc86c872bbb756
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|21862|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21862|  
|消息正文|无法使用同步方法 'database snapshot' 或 'database snapshot character' 在发布中发布 FILESTREAM 列。|  
  
## <a name="explanation"></a>解释  
由于无法通过数据库快照访问 FILESTREAM 数据，因此，为发布的同步方法指定 *database snapshot* 或 *database_snapshot_character* 参数时，快照代理将无法读取 FILESTREAM 数据。  
  
## <a name="user-action"></a>用户操作  
将发布的同步方法更改为 *database snapshot* 或 *database_snapshot_character* 以外的参数，或者只是在发布中排除 FILESTREAM 列。  
  
