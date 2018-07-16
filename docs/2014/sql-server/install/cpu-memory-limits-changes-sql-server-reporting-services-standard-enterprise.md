---
title: 对 SQL Server Reporting Services Standard 和 Enterprise 的 CPU 和内存限制更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dd553715-2b95-4119-8f58-d01de388d9ab
caps.latest.revision: 11
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2f2511d378113539bfe8a1a9ccab43da99334f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325447"
---
# <a name="changes-to-cpu-and-memory-limits-for-sql-server-reporting-services-standard-and-enterprise"></a>对 SQL Server Reporting Services Standard 和 Enterprise 的 CPU 和内存限制的更改
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services Standard 和 Enterprise 支持最多 64 GB 的系统内存。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
### <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services Standard 和 Enterprise 支持最多 64 GB 的系统内存。 您可能需要重新配置您的当前系统设置，以便顺应新的限制。  
  
 有关 CPU 和内存限制的其他版本的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[Compute Capacity Limits by Edition 的 SQL Server](../compute-capacity-limits-by-edition-of-sql-server.md)，和[SQL Server 各个版本支持内存](http://go.microsoft.com/fwlink/?LinkId=212633)。  
  
## <a name="corrective-action"></a>纠正措施  
 您可能需要重新配置您的当前系统设置，以便顺应新的 CPU 和内存限制。 有关详细信息，请参阅[ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)，和[服务器内存服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [后向兼容性](../../../2014/getting-started/backward-compatibility.md)  
  
  
