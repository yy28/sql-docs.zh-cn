---
title: GetCurrentCertificate 方法（SInstance）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetCurrentCertificate Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 9d2b72df-cb21-414a-abef-917f13d4de62
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5193a7a92df39b291ddbe69fec905cceb09f90a8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888542"
---
# <a name="getcurrentcertificate-method-sinstance-class"></a>GetCurrentCertificate 方法（SInstance 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.GetCurrentCertificate(SHA)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [实例上的服务器设置的](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) SInstance 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对象。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*SHA*|一个在方法完成后指定当前安全证书的字符串对象值（输出参数）。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
