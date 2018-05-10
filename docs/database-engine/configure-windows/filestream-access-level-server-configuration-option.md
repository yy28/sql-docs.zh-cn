---
title: “文件流访问级别”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c45a971793b03d30305adbb92d04e890f4dbc220
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  可以使用 filestream_access_level 选项来更改此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 FILESTREAM 访问级别。  
  
> [!NOTE]  
>  必须先启用 Windows FILESTREAM 管理设置，然后此选项才会生效。 可以在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时启用这些设置，也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器进行启用。  
  
|ReplTest1|定义|  
|-----------|----------------|  
|0|为此实例禁用 FILESTREAM 支持。|  
|@shouldalert|针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问启用 FILESTREAM。|  
|2|针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Win32 流访问启用 FILESTREAM。|  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎配置 - 文件流](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
