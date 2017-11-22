---
title: "在 SMO 中的向后兼容性 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a2d55e44e12fe3e4d57d2d1e8911899c51d1ce4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="backward-compatibility-in-smo"></a>SMO 中的向后兼容性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SMO 编写的应用程序使用早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以通过使用 SMO 中的重新编译[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
## <a name="migrating-smo-applications"></a>迁移 SMO 应用程序  
 必须删除对旧版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 SMO 动态链接库的引用，而且必须包括对随 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供的新 SMO 动态链接库的引用。  
  
 至少要引用以下内容：  
  
-   Microsoft.SqlServer.ConnectionInfo  
  
-   Microsoft.SqlServer.Smo  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc  
  
 连接类、SMO 实用工具类和基础类都需要这些文件。  
  
> [!NOTE]  
>  SmoEnum.dll 已被移除，所以，必须从 SMO [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 项目中移除对它的引用。  
  
 命名空间也已经更改，所以可以使用以下内容：  
  
##### <a name="for-visual-c"></a>对于 Visual C#  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
```  
  
##### <a name="for-visual-basic"></a>对于 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
```  
  
 如果你的代码使用 Urn 功能，如**Server.GetSqlSmoObject(Urn)**，你必须链接到 Microsoft.SqlServer.Management.Sdk.Sfc 命名空间。  
  
 如果您的代码直接使用 Transfer 对象，则需要链接到 Microsoft.SqlServer.Management.SmoExtended 命名空间。  
  
 迁移代码时，可能会需要修改代码。 这是因为有若干 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 功能在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中已不推荐使用。 有关弃用功能的详细信息，请参阅[SQL Server 2016 中不推荐使用数据库引擎功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)中[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]联机丛书。  
  
  
