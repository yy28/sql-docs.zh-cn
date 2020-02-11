---
title: 对 SQL Server Reporting Services Standard 和 Enterprise 的 CPU 和内存限制的更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: dd553715-2b95-4119-8f58-d01de388d9ab
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d8e18215c6078026b617e079879da1eadbca612
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095956"
---
# <a name="changes-to-cpu-and-memory-limits-for-sql-server-reporting-services-standard-and-enterprise"></a>对 SQL Server Reporting Services Standard 和 Enterprise 的 CPU 和内存限制的更改
  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services Standard 和 Enterprise 支持最多 64 GB 的系统内存。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
### <a name="description"></a>说明  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services Standard 和 Enterprise 支持最多 64 GB 的系统内存。 您可能需要重新配置您的当前系统设置，以便顺应新的限制。  
  
 有关的其他版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CPU 和内存限制的详细信息，请参阅[按版本的 SQL Server 计算容量限制](../compute-capacity-limits-by-edition-of-sql-server.md)和[SQL Server 版本支持的内存](https://go.microsoft.com/fwlink/?LinkId=212633)。  
  
## <a name="corrective-action"></a>纠正措施  
 您可能需要重新配置您的当前系统设置，以便顺应新的 CPU 和内存限制。 有关详细信息，请参阅[ALTER SERVER configuration &#40;transact-sql&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)和[服务器内存服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014 的各个版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [向后兼容性](../../../2014/getting-started/backward-compatibility.md)  
  
  
