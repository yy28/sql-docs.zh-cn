---
title: InstanceName 属性（ServerNetworkProtocolProperty）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- InstanceName Property (ServerNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- InstanceName property
ms.assetid: b3f24bf0-6b02-496b-b08e-327f7b320bc5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b933588a8d58b2f48c95e5bb0c2f1ede47944bbc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717216"
---
# <a name="instancename-property-servernetworkprotocolproperty-class"></a>InstanceName 属性（ServerNetworkProtocolProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  获取 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在其上安装了服务器网络协议的实例的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.InstanceName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [实例上的网络协议属性的](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) ServerNetworkProtocolProperty 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定对其安装服务器网络协议的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称的字符串值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
