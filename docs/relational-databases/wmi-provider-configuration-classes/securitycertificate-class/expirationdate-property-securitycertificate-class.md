---
title: ExpirationDate 属性 （SecurityCertificate 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExpirationDate Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExpirationDate property
ms.assetid: b7fbb9e9-85c1-475b-8e49-7c82fb3740aa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 93c8af9ebd709896da945246dbbc120ef4bd60ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088995"
---
# <a name="expirationdate-property-securitycertificate-class"></a>ExpirationDate 属性（SecurityCertificate 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取安全证书停止生效的日期。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ExpirationDate [= value]  
```  
  
## <a name="parts"></a>部件  
 *object*  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**uint32**值，该值指定安全证书的到期日期。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
