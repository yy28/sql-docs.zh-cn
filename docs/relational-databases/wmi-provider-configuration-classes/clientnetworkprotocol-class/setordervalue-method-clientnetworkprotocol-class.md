---
title: SetOrderValue 方法 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 161e733e89bfcd8593897483c97dd0d49dab8f18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040820"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 方法（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  从客户端协议列表中选择具有指定顺序值的协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## <a name="parts"></a>部件  
 *object*  
 一个表示 [客户端使用的网络协议的](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|描述|  
|---------------|-----------------|  
|*OrderValue*|一个设置顺序值的 u**int32** 值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [客户端协议属性（“顺序”选项卡）](https://technet.microsoft.com/library/ms187884.aspx)  
  
  
