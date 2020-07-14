---
title: “文件流访问级别”服务器配置选项 | Microsoft Docs
description: 熟悉“filestream_access_level”选项。 了解它如何更改 SQL Server 实例的 FILESTREAM 访问级别。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b891ba283acb1176a60bcc64105e126192aa8225
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772452"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level 服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  可以使用 filestream_access_level 选项来更改此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 FILESTREAM 访问级别。  
  
> [!NOTE]  
>  必须先启用 Windows FILESTREAM 管理设置，然后此选项才会生效。 可以在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时启用这些设置，也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器进行启用。  
  
|值|定义|  
|-----------|----------------|  
|0|为此实例禁用 FILESTREAM 支持。|  
|1|针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问启用 FILESTREAM。|  
|2|针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Win32 流访问启用 FILESTREAM。|  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎配置 - 文件流](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
