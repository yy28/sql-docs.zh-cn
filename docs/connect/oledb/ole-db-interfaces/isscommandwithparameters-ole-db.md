---
title: ISSCommandWithParameters (OLE DB) |Microsoft 文档
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
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
ms.openlocfilehash: c07f297668674c7f5f41e6ce30ff4ee692da660f
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689120"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSCommandWithParameters**接口公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)。 它是一个可选接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了从继承的三个方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供用于处理特定于服务器的数据类型的两种新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**时使用了服务组件，但服务组件不会使用此接口，可以使用接口。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|返回一个**SSPARAMPROPS**属性设置为传递到命令中，每个 UDT 或 XML 参数数组中的结构，但对于其他类型的参数返回 none。|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|序号，基于每个参数设置参数属性或通过指定的数组设置大容量参数属性**SSPARAMPROPS**结构。|  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [使用 XML 数据类型](../../oledb/features/using-xml-data-types.md)   
 [使用用户定义类型](../../oledb/features/using-user-defined-types.md)  
  
  
