---
title: NumberOfFlags 属性 （SInstance 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfFlags Property (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: b62005f8-9af3-4fc8-9344-a1ccdb713053
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e81ea322405352f5f78a29d0c7d45a8bd25307e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052528"
---
# <a name="numberofflags-property-sinstance-class"></a>NumberOfFlags 属性（SInstance 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取实例的标志数[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.NumberOfFlags [= value]  
```  
  
## <a name="parts"></a>部件  
 *object*  
 [SInstance 类](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md)对象，表示服务器实例。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**uint32**值，该值指定的标志的实例数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
