---
title: 刷新方法 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc59799077cd7c7c5039ada20a2dba54174d13c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-method-ado"></a>刷新方法 (ADO)
更新以反映，从可用的对象的集合和特定中的对象，提供程序。  
  
## <a name="syntax"></a>语法  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>注释  
 **刷新**方法完成不同的任务，具体取决于调用它的集合。  
  
### <a name="parameters"></a>Parameters  
 使用**刷新**方法[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合[命令](../../../ado/reference/ado-api/command-object-ado.md)对象检索存储过程的提供商端参数信息或中指定的参数化的查询**命令**对象。 集合将为空的提供程序不支持存储的过程调用或参数化的查询。  
  
 应设置[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性**命令**到有效的对象[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象， [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性一个有效命令，为和[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性**adCmdStoredProc**之前调用**刷新**方法。  
  
 如果你访问**参数**集合，然后再调用**刷新**方法，ADO 将自动调用方法并填充你的集合。  
  
> [!NOTE]
>  如果你使用**刷新**方法来获取参数信息来自提供程序和它返回一个或多个可变长度数据类型[参数](../../../ado/reference/ado-api/parameter-object.md)对象，ADO 可能会基于的参数分配内存其最大的潜在大小，这将导致在执行期间出错。 你应显式设置[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)之前调用这些参数的属性[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法，以防止出现错误。  
  
### <a name="fields"></a>字段  
 使用**刷新**方法[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合具有明显的效果。 若要从基础数据库结构中检索更改，你必须使用[Requery](../../../ado/reference/ado-api/requery-method.md)方法或者，如果[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象不支持书签， [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
### <a name="properties"></a>属性  
 使用**刷新**方法**属性**的某些对象的集合填充具有提供程序公开的动态属性的集合。 这些属性向以外内置属性 ADO 支持的提供程序提供有关特定功能的信息。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[轴集合](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[列集合](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[维度集合](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[错误集合](../../../ado/reference/ado-api/errors-collection-ado.md)|[字段集合](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[组集合](../../../ado/reference/adox-api/groups-collection-adox.md)|[层次结构集合](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[索引集合](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[键集合](../../../ado/reference/adox-api/keys-collection-adox.md)|[级别集合](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 集合](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[参数集合](../../../ado/reference/ado-api/parameters-collection-ado.md)|[位置集合](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[过程集合](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[属性集合](../../../ado/reference/ado-api/properties-collection-ado.md)|[表集合](../../../ado/reference/adox-api/tables-collection-adox.md)|[用户集合](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[视图集合](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另请参阅  
 [刷新方法示例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [刷新方法示例 （VC + +）](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count 属性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
