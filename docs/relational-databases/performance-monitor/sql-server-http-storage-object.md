---
title: SQL Server，HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2c0c2233b72c253f1bd2ab173a37f24703e02b4e
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158545"
---
# <a name="sql-server-http-storage"></a>SQL Server，HTTP 存储
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:HTTP Storage** 性能对象由监视 Microsoft Azure 存储帐户的性能计数器组成。 使用 [Microsoft Azure 中的 SQL Server 数据文件](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) 功能可以在 Windows Azure 存储 Blob 中存储数据库文件。 此性能对象将每一个 Windows Azure 存储帐户都视为不同的驱动器。  
  
|计数器名称|描述|  
|------------------|-----------------|  
|**页的Bytes/Read**|每次读取从 HTTP 存储传输的平均字节数。|  
|**页的Bytes/Transfer**|读取或写入操作过程中从 HTTP 存储传输的平均字节数。|  
|**页的Bytes/Write**|每次写入从 HTTP 存储传输的平均字节数。|  
|**Avg. microsec/Read**|每次从 HTTP 存储读取所用的平均微秒数。|  
|**Avg. microsec/Read Comp**|HTTP 完成读取存储所需平均微秒数。| 
|**Avg. microsec/Transfer**|每次向 HTTP 存储传输所用的平均微秒数。|  
|**Avg. microsec/Write**|每次向 HTTP 存储写入所用的平均微秒数。|  
|**Avg. microsec/Write Comp**|HTTP 完成写入存储所需平均微秒数。|  
|**HTTP Storage IO failed/sec**|每秒发送到 HTTP 存储的失败的写入请求数。| 
|**每秒的 HTTP 存储 I/O 重试次数**|每秒发送到 HTTP 存储的重试请求数。|  
|**Outstanding HTTP Storage I/O**|通往 HTTP 存储的待定 I/O 总数。|  
|**Read Bytes/sec**|读取操作过程中每秒从 HTTP 存储传输的数据量。|  
|**读取次数/秒**|每秒对 HTTP 存储的读取次数。|  
|**Total Bytes/sec**|读取或写入操作过程中每秒从 HTTP 存储传输的数据量。|  
|**Transfers/sec**|每秒对 HTTP 存储的读取和写入操作次数。|  
|**Write Bytes/sec**|写入操作过程中每秒从 HTTP 存储传输的数据量。|  
|**写入次数/秒**|每秒对 HTTP 存储的写入次数。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
