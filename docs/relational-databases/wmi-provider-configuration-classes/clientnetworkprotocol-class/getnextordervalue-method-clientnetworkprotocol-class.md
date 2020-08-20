---
description: GetNextOrderValue 方法（ClientNetworkProtocol 类）
title: 'GetNextOrderValue 方法 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetNextOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetNextOrderValue method
ms.assetid: d741dc5c-c225-43d9-a730-7ad664ac525f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b0ce809d245550b8dcc0b38e23415ff42257a476
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463664"
---
# <a name="getnextordervalue-method-clientnetworkprotocol-class"></a>GetNextOrderValue 方法（ClientNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  选择位于协议列表中的下一个位置的协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.GetNextOrderValue()  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示客户端使用的网络协议的 [ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)   
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
