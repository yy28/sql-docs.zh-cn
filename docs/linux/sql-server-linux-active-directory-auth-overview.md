---
title: 有关在 Linux 上的 SQL Server 的 active Directory 身份验证 |Microsoft 文档
description: 本文概述了在 Linux 上的 SQL server 的 Active Directory 身份验证。
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 8e53c238e83fe658aa0824547321183ec1c65885
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>有关在 Linux 上的 SQL Server 的 active Directory 身份验证

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供的 Active Directory (AD) 身份验证概述[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上。 AD 身份验证，则也称为集成身份验证中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 

## <a name="ad-authentication-overview"></a>AD 身份验证概述

AD 身份验证使在 Windows 或 Linux 进行身份验证到已加入域的客户端[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用其域凭据和 Kerberos 协议。

AD 身份验证通过具有以下优点[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证：

- 用户进行身份验证通过单一登录，而不会提示输入密码。   
- 通过创建的 AD 组的登录名，你可以管理访问和权限中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 组成员身份。  
- 每个用户组织，具有单个标识，因此不必能够跟踪其[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登录名对应于哪些用户。   
- AD，可在你的组织之间强制实施了集中式的密码策略。   

## <a name="configuration-steps"></a>配置步骤

若要使用 Active Directory 身份验证，你必须对你的网络的 AD 域控制器 (Windows)。

在教程中，提供了有关如何配置 AD 身份验证详细信息[教程： 在 Linux 上的 SQL 服务器的使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。 以下列表提供在本教程中的每个部分的链接的摘要：

1. [加入到 Active Directory 域的 SQL Server 主机](sql-server-linux-active-directory-authentication.md#join)。
1. [为 SQL Server 创建 AD 用户和设置 ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser)。
1. [配置 SQL Server 服务 keytab](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [在 TRANSACT-SQL 中创建基于 AD 的 SQL Server 登录名](sql-server-linux-active-directory-authentication.md#createsqllogins)。
1. [连接到 SQL Server 使用 AD 身份验证](sql-server-linux-active-directory-authentication.md#connect)。

## <a name="known-issues"></a>已知问题

- 在此期间，数据库镜像终结点支持的唯一身份验证方法是证书。 将在未来版本中启用 WINDOWS 身份验证方法。
- 第三方 AD 工具如 Centrify，Powerbroker，和不支持 Vintela。

## <a name="next-steps"></a>后续步骤

有关如何在 Linux 上实现 SQL Server 的 Active Directory 身份验证的详细信息，请参阅[教程： 在 Linux 上的 SQL 服务器的使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。