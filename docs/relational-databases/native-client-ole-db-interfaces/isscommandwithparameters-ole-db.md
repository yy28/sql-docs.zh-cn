---
title: "ISSCommandWithParameters (OLE DB) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords: ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70df9bbe13378f0e081ee03d8b1b9c6058c2afb9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSCommandWithParameters**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)。 这是一个可选接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了从继承的三个方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供用于处理服务器特定的数据类型的两种新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**时使用了服务组件，但服务组件本身将不使用此接口，可以使用接口。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|返回一个**SSPARAMPROPS**属性设置为传递到命令中，每个 UDT 或 XML 参数数组中的结构，但对于其他类型的参数返回 none。|  
|[ISSCommandWithParameters::SetParameterProperties &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|序号，基于每个参数设置参数属性或通过指定的数组设置大容量参数属性**SSPARAMPROPS**结构。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [使用 XML 数据类型](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [使用用户定义类型](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
