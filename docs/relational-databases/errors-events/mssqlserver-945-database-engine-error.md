---
title: MSSQLSERVER_945 | Microsoft Docs
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
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 49eb8e4472666be24a7edd1549dfe0e3705fd939
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|945|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DB_IS_SHUTDOWN|  
|消息正文|由于文件不可访问，或者内存或磁盘空间不足，所以无法打开数据库“%.*ls”。  有关详细信息，请参阅 SQL Server 错误日志。|  
  
## <a name="explanation"></a>解释  
由于缺少文件或其他资源，因此无法访问数据库。  
  
## <a name="user-action"></a>用户操作  
检查有关内存、磁盘空间或权限失败的其他信息的错误日志。 确认受影响数据库的 .mdf 和 .ndf 文件的位置，并确认由[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用的帐户拥有访问这些文件的权限。 更正问题后，使用 ALTER DATABASE 将数据库设置为 ONLINE，从而重新启动数据库。  
  

