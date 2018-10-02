---
title: “访问检查缓存”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 075cd37a349ea8d3900a235843657d89b71e8739
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763925"
---
# <a name="access-check-cache-server-configuration-options"></a>“访问检查缓存”服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问数据库对象时，访问检查缓存在一个名为 **访问检查结果缓存**的内部结构中。 **access check cache quota** 和 **access check cache bucket count** 选项控制用于 **访问检查结果缓存**的项数和哈希存储桶数。 在极少数情况下，可以通过更改这些选项来提高性能。  
  
 默认值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理这些选项。 Microsoft 建议仅在有 Microsoft 客户支持服务部门提供指导的情况下才更改这些选项。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
