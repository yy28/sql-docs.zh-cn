---
title: "ft notify bandwidth 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b02d56b6c9874a1d92524280f2f22ef9c7b190b4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>ft notify bandwidth 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 **ft notify bandwidth** 选项可以指定小内存缓冲区的池可以增长到的大小。 小内存缓冲区的大小为 64 千字节 (KB)。 *max* 参数值指定全文内存管理器在小缓冲池中应该维护的最大缓冲区数。 如果 **max** 值为零，则可以位于小缓冲池中的缓冲区数没有上限。  
  
 **min** 参数指定在小内存缓冲区的池中必须维护的最小内存缓冲区数。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存管理器发出请求后，将释放所有额外的缓冲池，但将保留该最低数量的缓冲区。 不过，如果指定的 **min** 值为零，则释放所有内存缓冲区。  
  
 在某些情况下，当前分配的缓冲区数小于 **min** 参数指定的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ft crawl bandwidth 服务器配置选项](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

