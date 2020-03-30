---
title: IClientVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: 本文提供了 IClientVirtualDeviceSet2::GetConfiguration 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5d7d42d081b0494feeb5c2b221575e0d5df1143a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847448"
---
# <a name="iclientvirtualdeviceset2getconfiguration-vdi"></a>IClientVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

GetConfiguration 函数用于等待服务器配置虚拟设备集  。

## <a name="syntax"></a>语法

```c
HRESULT IClientVirtualDeviceSet2::GetConfiguration (
   DWORD         dwTimeOut,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>parameters

*DwTimeOut* 此为超时时间（毫秒）。 使用 INFINITE 防止超时。

*pCfg* 执行成功后，此项将包含服务器所选的配置。 有关详细信息，请参阅“配置”。

## <a name="return-value"></a>返回值

|返回值 | 说明 |
|---|---|
| NOERROR | 已返回配置。 |
| VD_E_ABORT | 已调用 SignalAbort。 |
| VD_E_TIMEOUT | 函数超时。 |

## <a name="remarks"></a>备注

在可发出警报状态下此函数会阻塞。 调用成功后，虚拟设备集中的设备可能会打开。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。