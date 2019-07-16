---
title: SetCurrentCertificate 方法 （SInstance 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetCurrentCertificate Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 7349fb87-b973-4160-a2be-cab73abf5b31
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8a51d356ff5e16dfd64f0ba8b5f3b93bb593f2fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052551"
---
# <a name="setcurrentcertificate-method-sinstance-class"></a>SetCurrentCertificate 方法（SInstance 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetCurrentCertificate(SHA)  
```  
  
## <a name="parts"></a>部件  
 *object*  
 [SInstance 类](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md)对象，表示的实例上的服务器设置[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|描述|  
|---------------|-----------------|  
|*SHA*|一个指定当前安全证书的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
