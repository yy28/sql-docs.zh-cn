---
title: “访问检查缓存”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: feed895eeb7b11b4c41c51c4c26859a1057d2733
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158755"
---
# <a name="access-check-cache-server-configuration-options"></a>“访问检查缓存”服务器配置选项
通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问数据库对象时，访问检查缓存在一个名为 **访问检查结果缓存**的内部结构中。 
  
**访问检查缓存桶计数**选项控制用于访问检查结果缓存的哈希存储桶数。 

"**访问检查缓存配额**" 选项控制在访问检查结果缓存中存储的条目数。 达到最大条目数后，从访问检查结果缓存中删除最旧的条目。
  
默认值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理这些选项。 从 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ，默认值将转换为以下内部配置：
-   对于访问检查缓存 bucket 计数，值0将为 x86 体系结构设置默认值256存储桶，为 x64 和 IA-64 体系结构设置 2048 bucket。
-   对于访问检查缓存配额，值0会为 x86 体系结构设置默认值1024项，并为 x64 和 IA-64 体系结构设置 28192048 bucket。

在极少数情况下，可以通过更改这些选项来提高性能。 例如，如果使用了太多内存，则可能想要减小访问检查结果缓存的大小。 或者，如果在重新计算权限时 CPU 使用率过高，则可能需要增加访问检查结果缓存的大小。

> [!IMPORTANT]
> Microsoft 建议仅在有 Microsoft 客户支持服务部门提供指导的情况下才更改这些选项。
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
