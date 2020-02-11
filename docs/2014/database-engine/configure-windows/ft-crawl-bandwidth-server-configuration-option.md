---
title: ft crawl bandwidth 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f603987608a4c6456e01efc171bc93301069f046
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782173"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>ft crawl bandwidth 服务器配置选项
  使用 **ft crawl bandwidth** 选项可指定较大内存缓冲池可增长到多大。 较大内存缓冲区的大小为 4 MB。 
  **max** 参数值可指定全文内存管理器应在较大缓冲池中保持的最大缓冲区数。 如果 **max** 的值为零，则较大缓冲池中可以保持的缓冲区数没有上限。  
  
 
  **min** 参数可指定较大内存缓冲池中必须保持的最小内存缓冲区数。 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存管理器发出请求后，将释放所有额外的缓冲池，但将保留该最低数量的缓冲区。 不过，如果指定的 **min** 值为零，则释放所有内存缓冲区。  
  
 在某些情况下，当前分配的缓冲区数小于**min**参数指定的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [ft 通知带宽服务器配置选项](ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
