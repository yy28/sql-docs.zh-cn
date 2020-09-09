---
description: RemoveCertificate 方法（SInstance 类）
title: 'RemoveCertificate 方法 (SInstance) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- RemoveCertificate Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 7e5dbafa-a634-4617-9622-510514fce0ce
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0cfccfb29388a56df9fc6086b4d5a1f4618a4c89
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537101"
---
# <a name="removecertificate-method-sinstance-class"></a>RemoveCertificate 方法（SInstance 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例中删除当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.RemoveCertificate()  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [实例上的服务器设置的](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) SInstance 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
