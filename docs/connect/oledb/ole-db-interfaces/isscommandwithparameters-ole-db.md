---
title: ISSCommandWithParameters (OLE DB) |Microsoft 文档
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8942bc82c6f43be92740849eb607f3732585baa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters**接口公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)。 它是一个可选接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了从继承的三个方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供用于处理特定于服务器的数据类型的两种新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**时使用了服务组件，但服务组件不会使用此接口，可以使用接口。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|返回一个**SSPARAMPROPS**属性设置为传递到命令中，每个 UDT 或 XML 参数数组中的结构，但对于其他类型的参数返回 none。|  
|[ISSCommandWithParameters::SetParameterProperties & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|序号，基于每个参数设置参数属性或通过指定的数组设置大容量参数属性**SSPARAMPROPS**结构。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [使用 XML 数据类型](../../oledb/features/using-xml-data-types.md)   
 [使用用户定义的类型](../../oledb/features/using-user-defined-types.md)  
  
  
