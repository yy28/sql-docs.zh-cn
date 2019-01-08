---
title: “文件流访问级别”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 90b4ec97a3ab31c93e92219b96724b75d7f86425
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639273"
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
  
  
