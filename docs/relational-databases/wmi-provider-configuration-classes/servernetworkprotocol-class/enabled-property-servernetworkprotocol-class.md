---
title: 启用属性 （ServerNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: a514822a-91f1-4aca-9175-2b96cff29700
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0295185734443d1bd1e66d1a07543fa4fc2f0b34
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217835"
---
# <a name="enabled-property-servernetworkprotocol-class"></a>Enabled 属性（ServerNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取指定是否启用服务器网络协议的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ServerNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md)对象，表示使用的实例的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个布尔值，指定是否启用服务器网络协议： **，则返回 true**如果启用服务器网络协议，或**false**如果禁用服务器网络协议。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
