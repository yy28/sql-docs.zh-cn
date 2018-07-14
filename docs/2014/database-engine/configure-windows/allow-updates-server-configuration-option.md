---
title: “允许更新”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9acdfa9668a49ed5e0c67a932bacc1ccee1ac6b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196107"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 服务器配置选项
  此选项仍然存在于 **sp_configure** 存储过程中，但是其功能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中不可用。 其设置不起作用。 不支持直接更新系统表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 更改 **allow updates** 选项将导致 RECONFIGURE 语句失败。 应当从所有脚本中删除对 **allow updates** 选项的更改。  
  
## <a name="see-also"></a>请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
