---
description: SetCurrentCertificate 方法（ServerSettings 类）
title: 'SetCurrentCertificate 方法 (ServerSettings) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetCurrentCertificate Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: f9c6e172-11be-42de-b19b-a5b3436e84da
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 87b63717d6387302793269e14c239a2b5c066581
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544288"
---
# <a name="setcurrentcertificate-method-serversettings-class"></a>SetCurrentCertificate 方法（ServerSettings 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  设置当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetCurrentCertificate(SHA)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示实例上的服务器设置的 [ServerSettings 类](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*SHA*|一个指定当前安全证书的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
