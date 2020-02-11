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
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a82aa2872f5a1e1658ab3d736c2651253bb7cc74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62812040"
---
# <a name="access-check-cache-server-configuration-options"></a>“访问检查缓存”服务器配置选项
  通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问数据库对象时，访问检查缓存在一个名为 **访问检查结果缓存**的内部结构中。 **access check cache quota** 和 **access check cache bucket count** 选项控制用于 **访问检查结果缓存**的项数和哈希存储桶数。 在极少数情况下，可以通过更改这些选项来提高性能。  
  
 默认值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理这些选项。 Microsoft 建议仅在有 Microsoft 客户支持服务部门提供指导的情况下才更改这些选项。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
