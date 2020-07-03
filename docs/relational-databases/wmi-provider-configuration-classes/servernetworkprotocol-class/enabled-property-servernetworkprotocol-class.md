---
title: Enabled 属性（ServerNetworkProtocol）
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 755ef436a63a421fa2ee7ffaa335dee452d40d8b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888816"
---
# <a name="enabled-property-servernetworkprotocol-class"></a>Enabled 属性（ServerNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取指定是否启用服务器网络协议的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示实例使用的网络协议的[ServerNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 指定是否启用服务器网络协议的布尔值：如果启用了服务器网络协议，**则为 true** ; 如果禁用服务器网络协议，则为**false** 。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
