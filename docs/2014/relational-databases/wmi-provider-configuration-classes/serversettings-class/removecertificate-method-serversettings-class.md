---
title: RemoveCertificate 方法（ServerSettings 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- RemoveCertificate Method (ServerSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 9ffdbc39-93f5-48fb-859a-86a3ad545827
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 00731fab5c4bdec61848df93829dd5013a7454f5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056726"
---
# <a name="removecertificate-method-serversettings-class"></a>RemoveCertificate 方法（ServerSettings 类）
  从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例中删除当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.RemoveCertificate()  
  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [实例上的服务器设置的](serversettings-class.md) ServerSettings 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 u`int32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
