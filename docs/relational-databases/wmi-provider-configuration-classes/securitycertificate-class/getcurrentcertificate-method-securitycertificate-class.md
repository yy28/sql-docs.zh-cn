---
title: GetCurrentCertificate 方法 （SecurityCertificate 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 987a2671-1801-45c4-93e6-29f883c58720
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f18dcbb159975620f2d8eb8e8bf9b7472dcbec65
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672906"
---
# <a name="getcurrentcertificate-method-securitycertificate-class"></a>GetCurrentCertificate 方法（SecurityCertificate 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.GetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*SHA*|一个在方法完成后指定当前安全证书 SHA 指纹的字符串值（输出参数）。|  
|*SQLInstance*|一个为所需证书指定实例的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
