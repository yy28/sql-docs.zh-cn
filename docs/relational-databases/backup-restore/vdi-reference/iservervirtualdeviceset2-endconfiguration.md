---
title: IServerVirtualDeviceSet2::EndConfiguration
titlesuffix: SQL Server VDI reference
description: 本文提供了 IServerVirtualDeviceSet2::EndConfiguration 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d2ed7365e9a0e895a7deb0ba20d57868a947b350
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896330"
---
# <a name="iservervirtualdeviceset2endconfiguration-vdi"></a>IServerVirtualDeviceSet2::EndConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

EndConfiguration 函数通知 VDI 服务器已完成其配置  。

## <a name="syntax"></a>语法

```c
HRESULT IServerVirtualDeviceSet2::EndConfiguration ();
```

## <a name="return-value"></a>返回值

|返回值 | 说明 |
|---|---|
| NOERROR | 函数成功。 |
| VD_E_ABORT | 已请求中止。 |
| VD_E_PROTOCOL | 集未处于可配置状态。 |
| VD_E_MEMORY | 无法获取“RequestBuffers”调用所需的内存。 集仍处于可配置状态，且无可用的缓冲空间。 服务器可减少其缓冲区需求，或中止操作。 |

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。