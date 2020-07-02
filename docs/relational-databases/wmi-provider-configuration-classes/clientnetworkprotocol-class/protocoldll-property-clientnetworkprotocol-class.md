---
title: ProtocolDLL 属性（ClientNetworkProtocol）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9210b55a599d55759e5efcb7ca80a60385e9c69f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751519"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>ProtocolDLL 属性（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  获取[配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)指定的网络协议所需的 .dll 文件的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示客户端使用的网络协议的[ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络协议所需的协议 .dll 文件的字符串值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
