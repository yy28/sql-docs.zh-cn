---
title: SQL Server，HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a2a329f9c74baeac1996abd193a6b7d19c2263c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820013"
---
# <a name="sql-server-httpstorageobject"></a>SQL Server，HTTP_STORAGE_OBJECT
  **SQLServer:HTTP_STORAGE_OBJECT** 性能对象由监视 Windows Azure 存储帐户的性能计数器组成。 使用[在 Windows Azure 中的 SQL Server 数据文件](../databases/sql-server-data-files-in-microsoft-azure.md)功能，可以在 Windows Azure 存储 Blob 中存储数据库文件。 此性能对象将每一个 Windows Azure 存储帐户都视为不同的驱动器。  
  
|计数器名称|Description|  
|------------------|-----------------|  
|**Read Bytes/sec**|读取操作过程中每秒从 HTTP 存储传输的数据量。|  
|**Write Bytes/sec**|写入操作过程中每秒从 HTTP 存储传输的数据量。|  
|**Total Bytes/sec**|读取或写入操作过程中每秒从 HTTP 存储传输的数据量。|  
|**读取次数/秒**|每秒对 HTTP 存储的读取次数。|  
|**写入次数/秒**|每秒对 HTTP 存储的写入次数。|  
|**Transfers/sec**|每秒对 HTTP 存储的读取和写入操作次数。|  
|**平均Bytes/Read**|每次读取从 HTTP 存储传输的平均字节数。|  
|**页的Bytes/Write**|每次写入从 HTTP 存储传输的平均字节数。|  
|**页的Bytes/Transfer**|读取或写入操作过程中从 HTTP 存储传输的平均字节数。|  
|**Avg. microsec/Read**|每次从 HTTP 存储读取所用的平均微秒数。|  
|**Avg. microsec/Write**|每次向 HTTP 存储写入所用的平均微秒数。|  
|**Avg. microsec/Transfer**|每次向 HTTP 存储传输所用的平均微秒数。|  
|**Outstanding HTTP Storage I/O**|通往 HTTP 存储的待定 I/O 总数。|  
|**HTTP Storage I/O Retry/sec**|每秒发送到 HTTP 存储的重试请求数。|  
  
## <a name="see-also"></a>请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
