---
title: SystemStore 属性（SecurityCertificate）
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SystemStore Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SystemStore property
ms.assetid: 5d2a6ee2-d975-4fd6-adb5-ed43d0cc7fdd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 633cb01af0606671ee3d04663ec3cc40b589eaba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85625489"
---
# <a name="systemstore-property-securitycertificate-class"></a>SystemStore 属性（SecurityCertificate 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  获取安全证书的系统存储。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SystemStore [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个为安全证书指定系统存储的字符串值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
