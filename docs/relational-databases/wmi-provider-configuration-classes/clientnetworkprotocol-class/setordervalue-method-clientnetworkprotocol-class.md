---
description: SetOrderValue 方法（ClientNetworkProtocol 类）
title: 'SetOrderValue 方法 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1496143b862037ae8a4d0593ac3cc412dfd0b56e
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889095"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 方法（ClientNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  从客户端协议列表中选择具有指定顺序值的协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [客户端使用的网络协议的](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*OrderValue*|一个设置顺序值的 u**int32** 值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [客户端协议属性（“顺序”选项卡）](../../../tools/configuration-manager/client-protocols-properties-order-tab.md)  
  
