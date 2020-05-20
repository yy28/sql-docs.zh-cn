---
title: Refresh 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: rothja
ms.author: jroth
ms.openlocfilehash: 48fc3a1adf8dbeae010e4035ac4f2e390c015e54
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756537"
---
# <a name="refresh-method-ado"></a>Refresh 方法 (ADO)
更新集合中的对象，以反映提供程序提供的和特定于提供程序的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>备注  
 **Refresh**方法完成不同的任务，具体取决于调用该方法的集合。  
  
### <a name="parameters"></a>参数  
 对[command](../../../ado/reference/ado-api/command-object-ado.md)对象的[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合使用**Refresh**方法将检索在**命令**对象中指定的存储过程或参数化查询的提供程序端参数信息。 对于不支持存储过程调用或参数化查询的访问接口，该集合将为空。  
  
 在调用**Refresh**方法之前，应将**命令**对象的[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性设置为有效的[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，将[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性设置为有效的命令，并将[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性设置为**adCmdStoredProc** 。  
  
 如果在调用**Refresh**方法之前访问**参数**集合，则 ADO 将自动调用方法并填充集合。  
  
> [!NOTE]
>  如果使用**Refresh**方法从提供程序中获取参数信息，并返回一个或多个可变长度的数据类型[参数](../../../ado/reference/ado-api/parameter-object.md)对象，则 ADO 可能会根据其最大可能大小为参数分配内存，这将导致执行过程中出错。 在调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法以防止错误之前，应显式设置这些参数的[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)属性。  
  
### <a name="fields"></a>字段  
 对[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合使用**Refresh**方法不会产生任何效果。 若要从基础数据库结构中检索更改，必须使用[Requery](../../../ado/reference/ado-api/requery-method.md)方法，如果[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象不支持书签，则必须使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
### <a name="properties"></a>属性  
 对某些对象的**Properties**集合使用**Refresh**方法将使用提供程序公开的动态属性来填充集合。 这些属性提供了有关特定于提供程序的功能的信息，而不是 ADO 支持的内置属性。  
  
## <a name="applies-to"></a>应用于  
  
||||  
|-|-|-|  
|[轴集合](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[列集合](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[维度集合](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[错误集合](../../../ado/reference/ado-api/errors-collection-ado.md)|[字段集合](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[组集合](../../../ado/reference/adox-api/groups-collection-adox.md)|[层次结构集合](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[索引集合](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[键集合](../../../ado/reference/adox-api/keys-collection-adox.md)|[色阶集合](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[成员集合](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters 集合](../../../ado/reference/ado-api/parameters-collection-ado.md)|[位置集合](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[过程集合](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties 集合](../../../ado/reference/ado-api/properties-collection-ado.md)|[表集合](../../../ado/reference/adox-api/tables-collection-adox.md)|[用户集合](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[视图集合](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另请参阅  
 [Refresh 方法示例（VB）](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 方法示例（VC + +）](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count 属性（ADO）](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
