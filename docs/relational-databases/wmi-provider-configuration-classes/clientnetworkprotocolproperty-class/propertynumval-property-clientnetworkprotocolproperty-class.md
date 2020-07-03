---
title: PropertyNumVal 属性（ClientNetworkProtocolProperty）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyNumVal Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyNumVal property
ms.assetid: 12b02d97-702b-434f-baf6-e49a6b2cd4de
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d07e1efb01dd9109b130dc194929e60f8915c31a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888976"
---
# <a name="propertynumval-property-clientnetworkprotocolproperty-class"></a>PropertyNumVal 属性（ClientNetworkProtocolProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取[PropertyIdx 属性（ClientNetworkProtocolProperty 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md)值引用的当前属性的数值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyNumVal [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 表示客户端使用的网络协议属性的[ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)对象 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 u**int32**值，该值指定当前属性的数值。  
  
## <a name="remarks"></a>备注  
  
