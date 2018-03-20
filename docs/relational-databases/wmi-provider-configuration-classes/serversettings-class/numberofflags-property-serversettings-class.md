---
title: "NumberOfFlags 属性 （ServerSettings 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- NumberOfFlags Property (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumerOfFlags property
ms.assetid: d720f093-0d67-4e6c-8231-78d9ab853a8f
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef3e68ee7a2989b0d57479c1ceb83a4c71b4f8bd
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="numberofflags-property-serversettings-class"></a>NumberOfFlags 属性（ServerSettings 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取与实例相关联的常规标志数[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.NumberOfFlags [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示 [实例上的服务器设置的](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) ServerSettings 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 A **uint32**值，该值指定与实例相关联的常规标志数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
