---
title: “访问检查缓存”服务器配置选项 | Microsoft Docs
description: 了解访问检查结果缓存，以及控制该缓存行为的选项。 了解何时在 SQL Server 中更改这些选项。
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a389b84e673315a3c27f44c68a80092bf739d94b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751189"
---
# <a name="access-check-cache-server-configuration-options"></a>“访问检查缓存”服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问数据库对象时，访问检查缓存在一个名为 **访问检查结果缓存**的内部结构中。 **access check cache quota** 和 **access check cache bucket count** 选项控制用于 **访问检查结果缓存**的项数和哈希存储桶数。 在极少数情况下，可以通过更改这些选项来提高性能。  
  
 默认值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理这些选项。 Microsoft 建议仅在有 Microsoft 客户支持服务部门提供指导的情况下才更改这些选项。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
