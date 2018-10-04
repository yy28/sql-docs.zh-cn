---
title: “文件流访问级别”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8af40c988a9b994e1760ce59394dc1867e9da4c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120940"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level 服务器配置选项
  可以使用 filestream_access_level 选项来更改此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 FILESTREAM 访问级别。  
  
> [!NOTE]  
>  必须先启用 Windows FILESTREAM 管理设置，然后此选项才会生效。 可以在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时启用这些设置，也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器进行启用。  
  
|ReplTest1|定义|  
|-----------|----------------|  
|0|为此实例禁用 FILESTREAM 支持。|  
|1|针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问启用 FILESTREAM。|  
|2|针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Win32 流访问启用 FILESTREAM。|  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎配置 - 文件流](../../sql-server/install/database-engine-configuration-filestream.md)   
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
