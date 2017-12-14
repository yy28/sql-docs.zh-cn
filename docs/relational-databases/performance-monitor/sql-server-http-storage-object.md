---
title: "SQL Server，HTTP_STORAGE_OBJECT | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6519427db4b2e2fcb16826c1d595b132d7fb4e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-httpstorageobject"></a>SQL Server，HTTP_STORAGE_OBJECT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SQLServer:HTTP_STORAGE_OBJECT 性能对象由监视 Windows Azure 存储帐户的性能计数器组成。 使用 [Microsoft Azure 中的 SQL Server 数据文件](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) 功能可以在 Windows Azure 存储 Blob 中存储数据库文件。 此性能对象将每一个 Windows Azure 存储帐户都视为不同的驱动器。  
  
|计数器名称|说明|  
|------------------|-----------------|  
|**Read Bytes/sec**|读取操作过程中每秒从 HTTP 存储传输的数据量。|  
|**Write Bytes/sec**|写入操作过程中每秒从 HTTP 存储传输的数据量。|  
|**Total Bytes/sec**|读取或写入操作过程中每秒从 HTTP 存储传输的数据量。|  
|**读取次数/秒**|每秒对 HTTP 存储的读取次数。|  
|**写入次数/秒**|每秒对 HTTP 存储的写入次数。|  
|**Transfers/sec**|每秒对 HTTP 存储的读取和写入操作次数。|  
|**平均Bytes/Read**|每次读取从 HTTP 存储传输的平均字节数。|  
|**平均Bytes/Read BASE**|仅限内部使用。|
|**页的Bytes/Transfer**|读取或写入操作过程中从 HTTP 存储传输的平均字节数。|  
|**页的Bytes/Transfer BASE**|仅限内部使用。|
|**页的Bytes/Write**|每次写入从 HTTP 存储传输的平均字节数。|  
|**平均Bytes/Write BASE**|仅限内部使用。|
|**Avg. microsec/Read**|每次从 HTTP 存储读取所用的平均微秒数。|  
|**Avg. microsec/Read BASE**|仅限内部使用。|
|**Avg. microsec/Read Comp**|HTTP 完成读取存储所需平均微秒数。| 
|**Avg. microsec/Read Comp BASE**|仅限内部使用。|
|**Avg. microsec/Write**|每次向 HTTP 存储写入所用的平均微秒数。|  
|**Avg. microsec/Transfer**|每次向 HTTP 存储传输所用的平均微秒数。|  
|**Avg. microsec/Transfer BASE**|仅限内部使用。|
|**Avg. microsec/Write BASE**|仅限内部使用。|
|**Avg. microsec/Write Comp**|HTTP 完成写入存储所需平均微秒数。|  
|**Avg. microsec/Write Comp BASE**|仅限内部使用。|
|**Outstanding HTTP Storage I/O**|通往 HTTP 存储的待定 I/O 总数。|  
|**HTTP Storage IO failed/sec**|每秒发送到 HTTP 存储的失败的写入请求数。| 
|**HTTP Storage I/O Retry/sec**|每秒发送到 HTTP 存储的重试请求数。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
