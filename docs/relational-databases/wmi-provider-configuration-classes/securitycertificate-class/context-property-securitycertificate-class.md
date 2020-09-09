---
description: Context 属性（SecurityCertificate 类）
title: '上下文属性 (SecurityCertificate) '
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Context Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Context property
ms.assetid: 65dd737f-81ce-479e-8219-7b1b4d8f57c7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7e6c2c0d42e7b6d38e5a252cb8a1052fc87ed47b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545274"
---
# <a name="context-property-securitycertificate-class"></a>Context 属性（SecurityCertificate 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取安全证书的上下文。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Context [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定安全证书上下文的 **sint32** 数组值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
