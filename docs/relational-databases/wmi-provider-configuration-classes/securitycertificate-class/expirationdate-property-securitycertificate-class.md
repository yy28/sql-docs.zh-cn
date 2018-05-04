---
title: ExpirationDate 属性 （SecurityCertificate 类） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ExpirationDate Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExpirationDate property
ms.assetid: b7fbb9e9-85c1-475b-8e49-7c82fb3740aa
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fba3e58ec05633ebff63b3153c707a860346e88a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="expirationdate-property-securitycertificate-class"></a>ExpirationDate 属性（SecurityCertificate 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取安全证书停止生效的日期。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ExpirationDate [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 A **uint32**值，该值指定的安全证书的到期日期。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
