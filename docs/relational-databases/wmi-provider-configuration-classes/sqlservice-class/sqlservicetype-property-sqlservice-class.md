---
title: SqlServiceType 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: dbff2968-3011-41d6-a141-52d814af0213
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 12e285e4348c2fac373797d4e260ea088facaabf
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675606"
---
# <a name="sqlservicetype-property-sqlservice-class"></a>SqlServiceType 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取托管服务的类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SqlServiceType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
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
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
