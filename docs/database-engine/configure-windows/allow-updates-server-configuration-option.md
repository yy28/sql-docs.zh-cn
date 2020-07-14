---
title: “允许更新”服务器配置选项 | Microsoft Docs
description: 了解“允许更新”这一已过时的 SQL Server 配置选项。 了解为何使用此选项将导致 RECONFIGURE 语句失败。
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6e4cde898f4b7c95fa3dd46d23d073ba47b5fb43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725264"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  此选项仍然存在于 **sp_configure** 存储过程中，但是其功能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中不可用。 其设置不起作用。 不支持直接更新系统表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 更改 **allow updates** 选项将导致 RECONFIGURE 语句失败。 应当从所有脚本中删除对 **allow updates** 选项的更改。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
