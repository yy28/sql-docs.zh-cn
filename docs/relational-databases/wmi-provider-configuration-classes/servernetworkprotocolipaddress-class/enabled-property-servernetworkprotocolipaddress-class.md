---
title: 启用属性 （ServerNetworkProtocolIpAddress 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f6562c4985edd9379a4ca330772e56bb566c67a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911927"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 属性（ServerNetworkProtocolIpAddress 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取指定是否启用 IP 地址的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>部件  
 *object*  
 一个[ServerNetworkProtocolIPAdress 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md)对象，表示的实例上的网络协议 IP 地址[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个布尔值，指定是否启用了 IP 地址： **，则返回 true**如果启用了 IP 地址，或**false**如果 IP 地址处于禁用状态。  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
