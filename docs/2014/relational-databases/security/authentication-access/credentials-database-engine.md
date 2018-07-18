---
title: 凭据（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 579b9d6f9847652ab2088eeb5111372fc4377c02
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198777"
---
# <a name="credentials-database-engine"></a>凭据（数据库引擎）
  凭据是包含连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部资源所需的身份验证信息（凭据）的记录。 此信息由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在内部使用。 大多凭据都包含一个 Windows 用户名和密码。  
  
 利用凭据中存储的信息，通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证方式连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的用户可以访问服务器实例外部的资源。 如果外部资源为 Windows，则此用户将作为在凭据中指定的 Windows 用户通过身份验证。 单个凭据可映射到多个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。 但是，一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名只能映射到一个凭据。  
  
 系统凭据是自动创建的，并与特定端点关联， 系统凭据名以两个哈希符号 (##) 开头。  
  
 有关凭据的详细信息，请参阅[sys.credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql)目录视图。  
  
## <a name="related-content"></a>相关内容  
 [创建凭据](../authentication-access/create-a-credential.md)[创建凭据&#40;Transact SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [保护 SQL Server](../securing-sql-server.md)  
  
  
