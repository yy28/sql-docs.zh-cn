---
description: StartMode 属性（SqlService 类）
title: 'StartMode 属性 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 608214cf9d4eca2601c0f8bee7b82570ec936ea6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418753"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 属性（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取服务的启动模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务模式的 uint32 值。  
  
 可以是下列值之一。  
  
 启动  
 值 = 0。 服务由操作系统加载程序启动。 此选项只对驱动程序服务有效。  
  
 系统  
 值 = 1。 由 **IoInitSystem** 方法启动的服务。 此选项只对驱动程序服务有效。  
  
 自动  
 值 = 2。 服务将在系统启动期间由服务控制管理器自动启动。  
  
 手动  
 值 = 3。 要在进程调用 **StartService** 方法时由计算机管理器启动的服务。  
  
 已禁用  
 值 = 4。 无法启动服务。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
