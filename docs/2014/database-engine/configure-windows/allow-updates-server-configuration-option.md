---
title: “允许更新”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6cf28b18bcad06be7383b98dee72810c4e6157c0
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52641206"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 服务器配置选项
  此选项仍然存在于 **sp_configure** 存储过程中，但是其功能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中不可用。 其设置不起作用。 不支持直接更新系统表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 更改 **allow updates** 选项将导致 RECONFIGURE 语句失败。 应当从所有脚本中删除对 **allow updates** 选项的更改。  
  
## <a name="see-also"></a>请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
