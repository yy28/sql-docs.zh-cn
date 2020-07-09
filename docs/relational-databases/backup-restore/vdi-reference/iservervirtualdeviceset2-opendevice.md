---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: 本文提供了 IServerVirtualDeviceSet2::OpenDevice 命令的参考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b43f2adedde0c317f24ee811c4ac1b2a69057de2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898927"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**OpenDevice** 函数从虚拟设备集获取虚拟设备接口。

## <a name="syntax"></a>语法

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>parameters

*lpName* 这是 BACKUP 或 RESTORE 命令的第一个 VIRTUAL_DEVICE= 子句提供的。 此名称用作访问客户端创建的虚拟设备集的密钥。

*ppVirtualDevice* 用于返回虚拟设备接口。

## <a name="return-value"></a>返回值

|返回值 | 说明 |
|---|---|
| NOERROR | 函数成功。 |
| VD_E_OPEN |所有设备都已打开。 |

## <a name="remarks"></a>备注

每次调用都将返回下一个未打开的设备。 该函数的调用次数必须与虚拟设备集配置中指定的设备数相同。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [SQL Server 虚拟设备接口引用概述](reference-virtual-device-interface.md)。