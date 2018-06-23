---
title: SQL Server 复制中不推荐使用的功能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deprecated features [SQL Server replication]
ms.assetid: 46bd3edd-d6de-40a6-a015-21cce8321feb
caps.latest.revision: 64
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1c0a7579c8d895c398b1a7d75df56f3ffa2d1d04
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029209"
---
# <a name="deprecated-features-in-sql-server-replication"></a>SQL Server 复制中不推荐使用的功能
  本主题介绍 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中仍然可用但不推荐使用的复制功能。 按照计划， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未来版本将不再具有这些功能。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
## <a name="items-deprecated-in-sql-server-2014"></a>SQL Server 2014 中不推荐使用的项  
  
|功能|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|如果每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 端点都处于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的当前版本的两个主版本内，则支持复制。 因此， [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 不支持面向或源自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的复制。|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)]|如果每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 端点都处于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的当前版本的两个主版本内，则支持复制。 因此， [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 不支持面向或源自 [!INCLUDE[ssEW](../../includes/ssew-md.md)]的复制。|  
  
## <a name="see-also"></a>请参阅  
 [复制的向后兼容性](replication-backward-compatibility.md)  
  
  