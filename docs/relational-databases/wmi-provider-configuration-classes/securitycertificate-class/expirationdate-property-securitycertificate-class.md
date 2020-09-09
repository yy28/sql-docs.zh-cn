---
description: ExpirationDate 属性（SecurityCertificate 类）
title: 'ExpirationDate 属性 (SecurityCertificate) '
ms.custom: seo-lt-2019
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e1340521a683dc410572cb34f2d4ef8daaab9513
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537777"
---
# <a name="expirationdate-property-securitycertificate-class"></a>ExpirationDate 属性（SecurityCertificate 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取安全证书停止生效的日期。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ExpirationDate [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定安全证书的过期日期的 **uint32** 值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
