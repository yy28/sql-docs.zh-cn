---
title: "max full-text crawl range 服务器配置选项 | Microsoft Docs"
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
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81514b4562657bb01d5d0ec841dc5e6ec1865099
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>max full-text crawl range 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 **max full-text crawl range** 选项可以优化 CPU 使用率，从而提高完全爬网时的爬网性能。 使用此选项，可以指定索引完全爬网时 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的分区数。 例如，如果有许多 CPU 且它们的使用率并非最佳，则可以增加此选项的最大值。 除了此选项以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还使用众多其他因素（如表中的行数和 CPU 数）来确定应该使用的实际分区数。  
  
 此选项的默认值是 4；最小值是 1，最大值是 256。 对此选项所做的更改只会影响后续的爬网。 不会影响正在进行的爬网。  
  
 **max full-text crawl range** 选项是一个高级选项。 如果使用 **sp_configure** 系统存储过程来更改该设置，则仅当 **显示高级选项** 设置为 1 时才能更改 **max full-text crawl range** （全文爬网最大范围）。 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

