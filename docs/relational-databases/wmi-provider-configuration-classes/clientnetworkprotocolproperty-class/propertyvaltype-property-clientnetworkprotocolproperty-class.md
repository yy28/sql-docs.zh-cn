---
title: PropertyValType 属性（ClientNetworkProtocolProperty）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyValType Property (ClientNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyValType property
ms.assetid: 624b9bdd-ed93-4140-bd4e-00d714a2558c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 193df6ad932a4eeb496f696f15ff100b74584d00
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888942"
---
# <a name="propertyvaltype-property-clientnetworkprotocolproperty-class"></a>PropertyValType 属性（ClientNetworkProtocolProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取[PropertyIdx 属性（ClientNetworkProtocolProperty 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md)值引用的属性中存储的值的数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyValType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 表示客户端使用的网络协议属性的[ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 指定属性值的数据类型的**uint32**值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
