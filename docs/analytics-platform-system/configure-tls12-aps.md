---
title: 配置 TLS 1。2
description: 在 AP 中配置 TLS 1.2 的建议
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 988cac765a596b541d128b0b6190f6f228d95ee7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401256"
---
# <a name="configure-tls-12-in-aps"></a>在 AP 中配置 TLS 1。2

若要保护仅使用 TLS 1.2 的 AP，必须在所有物理主机和虚拟主机上显式禁用其他协议。 禁用协议需要更改注册表设置。 注册表更改需要重新启动虚拟主机和物理主机。

> [!WARNING]
> 本节、方法或任务所含的步骤告知您如何修改注册表。 但是，如果错误地修改了可能会导致数据丢失并要求重新安装操作系统的注册表，则可能会出现严重问题。 我们强烈建议在修改注册表之前对其进行备份。 如果发生问题，以后可还原注册表。 有关如何备份和还原注册表的详细信息，请单击以下文章编号以查看 Microsoft 知识库中的文章：<br>
[322756](https://support.microsoft.com/help/322756)如何在 Windows 中备份和还原注册表

**禁用**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

还应在客户端计算机上设置以下密钥，其中安装了与 AP SSIS 目标适配器类似的工具。
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



