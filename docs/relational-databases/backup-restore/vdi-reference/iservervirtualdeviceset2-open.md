---
title: IServerVirtualDeviceSet2::Open
titlesuffix: SQL Server VDI reference
description: 本文提供了 IServerVirtualDeviceSet2::Open 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 552394db26a1b236a4d6997f6dbfba77d12086ee
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847218"
---
# <a name="iservervirtualdeviceset2open-vdi"></a>IServerVirtualDeviceSet2::Open (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Open 函数打开服务器上的虚拟设备集，该函数必须是使用 COM 提供的接口句柄进行的首次调用  。

## <a name="syntax"></a>语法

```c
HRESULT IServerVirtualDeviceSet2::Open (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpName
);
```

## <a name="parameters"></a>parameters

*lpInstanceName* 此字符串标识将向其发送 SQL 命令的 SQL Server 实例。 可以传递 NULL 来标识当前计算机上的默认实例。

*lpName* 这是 BACKUP 或 RESTORE 命令的第一个 VIRTUAL_DEVICE= 子句提供的。 此名称用作访问客户端创建的虚拟设备集的密钥。

## <a name="return-value"></a>返回值

|返回值 | 说明 |
|---|---|
| NOERROR | 函数成功。 |
| VD_E_INVALID | 提供的名称未标识服务器可访问的虚拟设备集。 |

## <a name="remarks"></a>备注

成功调用此函数后，服务器可以继续使用 GetConfiguration 和 SetConfiguration 配置虚拟设备集。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。