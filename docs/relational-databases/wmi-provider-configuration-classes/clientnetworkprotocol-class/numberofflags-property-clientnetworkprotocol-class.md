---
title: NumberOfFlags 属性（ClientNetworkProtocol）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfFlags Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd30518f441dc2f54e65c838911503fd6d57fd56
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889046"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 属性（ClientNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取由[SetOrderValue 方法（ClientNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md)指定的客户端网络协议所需的标志选项的数目。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [客户端使用的网络协议的](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**Uint32**值，指定**OrderValue**属性所引用的客户端网络协议所需的标志选项数。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
