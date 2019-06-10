---
title: “允许更新”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 2be9a6eb16bf2b4f481faf6409b28da11eb39eb5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799573"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此选项仍然存在于 **sp_configure** 存储过程中，但是其功能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中不可用。 其设置不起作用。 不支持直接更新系统表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 更改 **allow updates** 选项将导致 RECONFIGURE 语句失败。 应当从所有脚本中删除对 **allow updates** 选项的更改。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
