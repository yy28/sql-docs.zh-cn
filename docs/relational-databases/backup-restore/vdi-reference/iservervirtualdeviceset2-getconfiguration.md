---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: 本文提供了 IServerVirtualDeviceSet2::GetConfiguration 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1d62a2042221bebf04e19a46a21ba81caa7c877b
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847248"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

GetConfiguration 函数获取客户端请求的配置  。

## <a name="syntax"></a>语法

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>Parameters

*pCfg* 这是客户端使用 IClientVirtualDeviceSet2::Create 指定的配置。

## <a name="return-value"></a>返回值

返回 *HRESULT* ，指示方法调用是成功还是失败。 值 NOERROR 指示方法调用已成功。 非零值指示已发生错误。

## <a name="remarks"></a>Remarks

服务器需要检查并响应客户端提供的设置。 有关详细信息，请参阅“配置”。 如果服务器确定它无法使用提供的配置正常运行，则可以使用 SignalAbort。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。