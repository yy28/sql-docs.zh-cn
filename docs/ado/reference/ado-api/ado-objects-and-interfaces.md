---
title: ADO 对象和接口 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 48b1f3794828af7f60c1d00313506fa9f9c522c8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696633"
---
# <a name="ado-objects-and-interfaces"></a>ADO 对象和接口
在中表示这些对象之间的关系[ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)。  
  
 每个对象可以包含在其相应的集合。 例如，[错误](../../../ado/reference/ado-api/error-object.md)对象可以包含在[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合。 有关详细信息，请参阅[ADO 集合](../../../ado/reference/ado-api/ado-collections.md)或特定集合的主题。  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|用于从 ADOCommand 对象检索基础 OLEDB 命令。|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|构造一个 ADO**记录**对象从 OLE DB**行**C 中的对象 /C++应用程序。|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|构造一个 ADO**记录集**对象从 OLE DB**行集**C 中的对象 /C++应用程序。|  
|[ADOStreamConstruction 接口](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|构造一个 ADO **Stream**对象从 OLE DB **IStream** C 中的对象 /C++应用程序。|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|定义要对数据源执行的特定命令。<br /><br /> **命令**对象不是可安全执行脚本。|  
|[“连接”](../../../ado/reference/ado-api/connection-object-ado.md)|表示与数据源的开放连接。<br /><br /> **连接**对象是可安全执行脚本。|  
|[IDSOShapeExtensions 接口](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|获取形状提供程序的基础的 OLEDB 数据源对象。|  
|[错误](../../../ado/reference/ado-api/error-object.md)|包含有关适用于单个操作涉及该提供程序的数据访问错误的详细信息。<br /><br /> **错误**对象不是可安全执行脚本。|  
|[字段](../../../ado/reference/ado-api/field-object.md)|表示与常见的数据类型的数据的列。|  
|[参数](../../../ado/reference/ado-api/parameter-object.md)|表示参数或参数与相关联**命令**对象基于参数化的查询或存储的过程。<br /><br /> **参数**对象不是可安全执行脚本。|  
|[属性](../../../ado/reference/ado-api/property-object-ado.md)|表示由提供程序定义的 ADO 对象的动态特征。|  
|[记录](../../../ado/reference/ado-api/record-object-ado.md)|表示的行**记录集**，目录或文件系统中的文件。 **记录**对象是可安全执行脚本。|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|表示从基础表或执行命令的结果的记录集。 任何时候**记录集**对象是指仅为当前记录集内的单个记录。<br /><br /> **记录集**对象是可安全执行脚本。|  
|[流](../../../ado/reference/ado-api/stream-object-ado.md)|表示数据的二进制流。<br /><br /> **Stream**对象是可安全执行脚本。|  
  
## <a name="see-also"></a>请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 动态属性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 B：ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
