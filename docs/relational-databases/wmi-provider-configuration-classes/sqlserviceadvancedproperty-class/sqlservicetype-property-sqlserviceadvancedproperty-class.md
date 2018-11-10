---
title: SqlServiceType 属性 （SqlServiceAdvancedProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5d75ed668424f99b9bee1654799c5646741714fe
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216165"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType 方法（SqlServiceAdvancedProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取与高级属性关联的托管服务的类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务类型的 uint32 值。  
  
## <a name="remarks"></a>备注  
 返回值可以是下列值之一：  
  
|类型|定义|  
|----------|----------------|  
|*1*|MSSQLSERVER 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务。|  
|*2*|SQLSERVERAGENT 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服务。|  
|*3*|MSFTESQL 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Full-text Search Engine 服务。|  
|*4*|MsDtsServer 为 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 服务。|  
|*5*|MSSQLServerOLAPService 为 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务。|  
|*6*|ReportServer 为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 服务。|  
|*7*|SQLBrowser 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser 服务。|  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
