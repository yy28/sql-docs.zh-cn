---
title: "“允许更新”服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9eb06b2859684d71ba260879aa966e5e4fe8073
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此选项仍然存在于 **sp_configure** 存储过程中，但是其功能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中不可用。 其设置不起作用。 不支持直接更新系统表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 更改 **allow updates** 选项将导致 RECONFIGURE 语句失败。 应当从所有脚本中删除对 **allow updates** 选项的更改。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
