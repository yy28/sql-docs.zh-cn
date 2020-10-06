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
ms.openlocfilehash: 04205ee05e3c26cc807a3a6aa828152c20e4c3c7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670947"
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
 [数据库引擎配置 - 文件流](../install-windows/install-sql-server.md)   
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
