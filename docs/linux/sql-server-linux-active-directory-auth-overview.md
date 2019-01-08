---
title: Linux 上的 SQL Server 的 active Directory 身份验证
titleSuffix: SQL Server
description: 本文概述了 Linux 上的 SQL Server 的 Active Directory 身份验证。
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: fcc2148119634c7114d72f67b2c7143fa7d47724
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160395"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Linux 上的 SQL Server 的 active Directory 身份验证

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供的 Active Directory (AD) 身份验证的概述[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 上。 AD 身份验证也称为是集成的身份验证中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 

## <a name="ad-authentication-overview"></a>AD 身份验证概述

AD 身份验证，在 Windows 或 Linux 进行身份验证到已加入域的客户端[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用其域凭据和 Kerberos 协议。

AD 身份验证通过具有以下优点[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证：

- 用户进行身份验证通过单一登录，而不会提示输入密码。   
- 通过创建的 AD 组的登录名，你可以管理访问和权限中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 组成员身份。  
- 每个用户在组织内具有单一标识，因此无需跟踪的这[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登录名对应于它们的用户。   
- AD，可在你的组织强制使用集中式的密码策略。   

## <a name="configuration-steps"></a>配置步骤

若要使用 Active Directory 身份验证，必须在网络上具有 AD 域控制器 (Windows)。

在本教程中，提供了有关如何配置 AD 身份验证详细信息[教程：使用 Active Directory 身份验证与 Linux 上的 SQL Server](sql-server-linux-active-directory-authentication.md)。 在本教程中，以下列表提供了指向每个部分的摘要：

1. [加入到 Active Directory 域的 SQL Server 主机](sql-server-linux-active-directory-authentication.md#join)。
1. [为 SQL Server 创建 AD 用户并设置 ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser)。
1. [配置 SQL Server 服务 keytab](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [在 TRANSACT-SQL 中创建基于 AD 的 SQL Server 登录名](sql-server-linux-active-directory-authentication.md#createsqllogins)。
1. [连接到 SQL Server 使用 AD 身份验证](sql-server-linux-active-directory-authentication.md#connect)。

## <a name="known-issues"></a>已知问题

- 在此期间，数据库镜像终结点支持的唯一身份验证方法是证书。 将在将来的版本中启用 WINDOWS 身份验证方法。

## <a name="next-steps"></a>后续步骤

有关如何在 Linux 上实现 SQL Server 的 Active Directory 身份验证的详细信息，请参阅[教程：使用 Active Directory 身份验证与 Linux 上的 SQL Server](sql-server-linux-active-directory-authentication.md)。
