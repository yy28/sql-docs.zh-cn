---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: 本文提供了 IServerVirtualDeviceSet2::FreeBuffer 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2829f849ce8cd220fdabc75a0d2059c5da0c80fd
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847258"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

FreeBuffer 函数获取虚拟设备集的共享内存缓冲区  。

## <a name="syntax"></a>语法

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>Parameters

*pBuffer* 返回由 IServerVirtualDeviceSet2::AllocateBuffer 返回的缓冲区。

*dwSize* 这是缓冲区的大小（以字节为单位）。 不包括客户端请求的任何前缀区域。 任何此类区域对服务器都是隐藏的，并且在返回缓冲地址之前会有可用空间。

## <a name="return-value"></a>返回值

|返回值 | 解释 |
|---|---|
| NOERROR | 已返回缓冲区。 |
| VD_E_INVALID | 参数无效。 |

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。