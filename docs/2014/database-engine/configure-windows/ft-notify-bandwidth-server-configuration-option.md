---
title: ft notify bandwidth 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 614bbbf4520ee0e1dd7cced276ca2a69ca948c48
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198247"
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>ft notify bandwidth 服务器配置选项
  使用 **ft notify bandwidth** 选项可以指定小内存缓冲区的池可以增长到的大小。 小内存缓冲区的大小为 64 千字节 (KB)。 *max* 参数值指定全文内存管理器在小缓冲池中应该维护的最大缓冲区数。 如果`max`值为零，则可以位于小缓冲池中的缓冲区数没有上限。  
  
 **min** 参数指定在小内存缓冲区的池中必须维护的最小内存缓冲区数。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存管理器发出请求后，将释放所有额外的缓冲池，但将保留该最低数量的缓冲区。 不过，如果指定的 **min** 值为零，则释放所有内存缓冲区。  
  
 在某些情况下，当前分配的缓冲区数小于 **min** 参数指定的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [ft crawl bandwidth 服务器配置选项](ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
