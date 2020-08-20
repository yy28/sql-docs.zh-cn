---
description: State 属性（SqlService 类）
title: '状态属性 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- State Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 606c991cd1f5b20f888fc2a2bf9d500e4e5ec410
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485058"
---
# <a name="state-property-sqlservice-class"></a>State 属性（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取或设置服务的当前状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务状态的 uint32 值。  
  
 可以是下列值之一。  
  
 1  
 已停止。 服务已停止。  
  
 2  
 启动挂起。 服务正在等待启动。  
  
 3  
 停止挂起。 服务正在等待停止。  
  
 4  
 正在运行。 服务正在运行。  
  
 5  
 继续挂起。 服务正在等待继续。  
  
 6  
 暂停挂起。 服务正在等待暂停。  
  
 7  
 已暂停。 服务已暂停。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
