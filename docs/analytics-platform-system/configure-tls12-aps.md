---
title: '在分析平台系统中配置 TLS 1.2 |Microsoft Docs '
description: 建议在 AP 中配置 TLS 1.2
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6ea2144fe333f87123abdf92e16aa7122e98b4
ms.sourcegitcommit: 0f452eca5cf0be621ded80fb105ba7e8df7ac528
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007550"
---
# <a name="configure-tls-12-in-aps"></a>在 AP 中配置 TLS 1.2

若要保护 APS 为仅使用 TLS 1.2，必须要明确禁用所有物理和虚拟的主机上的其他协议。 禁用协议需要进行注册表设置更改。 注册表更改需要重新启动的虚拟和物理主机。

> [!WARNING]
> 本节、方法或任务所含的步骤告知您如何修改注册表。 但是，如果修改了注册表不正确，可能会导致数据丢失并需要重新安装操作系统的则可能会出现严重问题。 我们强烈建议备份注册表之前对其进行修改。 如果发生问题，以后可还原注册表。 有关如何备份和还原注册表的详细信息，请单击下面的文章编号，以查看 Microsoft 知识库中相应的文章：<br>
[322756](https://support.microsoft.com/help/322756)如何备份和还原 Windows 中的注册表

**禁用：**
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

此外设置以下项在你的客户端上机 APS SSIS 目标适配器之类的工具的安装位置。
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



