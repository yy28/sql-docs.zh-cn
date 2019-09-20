---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: 本文提供了 IServerVirtualDevice::CloseDevice 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c73649e2a4301e94f8e68504222cc0122061f25f
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847428"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

CloseDevice 函数可关闭使用 IServerVirtualDeviceSet2::OpenDevice 函数打开的虚拟设备 

## <a name="syntax"></a>语法

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>返回值

|返回值 | 解释 |
|---|---|
| VD_E_CLOSE | 设备已关闭。 |
| VD_E_ABORT | 接口处于中止状态。 |

## <a name="remarks"></a>Remarks

使用 SignalAbort 强制进行异常终止后，不需要 CloseDevice 。 如果在使用 SignalAbort 后调用 CloseDevice，则不会执行任何操作。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。