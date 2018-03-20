---
title: "SetCurrentCertificate 方法 （SecurityCertificate 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f1c5c41f15a76d796fce09b4a6db92e9ef7a3d3
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>SetCurrentCertificate 方法（SecurityCertificate 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示安全证书的 [SecurityCertificate 类](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*SHA*|一个为所需安全证书指定安全哈希算法 (SHA) 指纹的字符串值。|  
|*SQLInstance*|一个为所需证书指定实例的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
