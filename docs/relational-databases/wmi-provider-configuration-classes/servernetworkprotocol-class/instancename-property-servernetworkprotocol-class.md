---
title: InstanceName 属性 （ServerNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- InstanceName Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- InstanceName property
ms.assetid: 456911c1-9881-4574-8576-0070eff78c27
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 94bc041315adacf2dfea4f37fd61db83426221ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834525"
---
# <a name="instancename-property-servernetworkprotocol-class"></a>InstanceName 属性（ServerNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取的实例的名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所引用的服务器网络协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.InstanceName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ServerNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md)对象，表示使用的实例的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务器网络协议引用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称的字符串值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
