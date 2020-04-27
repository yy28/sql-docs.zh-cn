---
title: SetDisable 方法（ServerNetworkProtocolIPAddress 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetDisable Method (ServerNetworkProtocolIPAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: 7a7cc8cc-9fb8-4bf5-b483-2150d633ee10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: adaa66fd04f6e3b6f97b4e4edc75d9a21ea4e31f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62643218"
---
# <a name="setdisable-method-servernetworkprotocolipaddress-class"></a>SetDisable 方法（ServerNetworkProtocolIPAddress 类）
  禁用 IP 地址。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示实例上的网络协议 IP 地址的 [ServerNetworkProtocolIPAdress Class] servernetworkprotocolipaddress-class.md）对象[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
