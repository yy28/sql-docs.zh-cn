---
title: "方法签名 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e7650cb3516311f3eb93e93304ba9d20ec874466
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="nextrecordset-method-ado"></a>方法签名 (ADO)
清除当前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象并返回下一个**记录集**方法通过一系列的命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>返回值  
 返回**记录集**对象。 在语法模型中， *recordset1*和*recordset2*可以相同**记录集**对象，也可以使用单独的对象。 当使用单独**记录集**对象，重置**ActiveConnection**原始属性**记录集**(*recordset1*)后**签名**已调用将生成错误。  
  
#### <a name="parameters"></a>Parameters  
 *RecordsAffected*  
 可选。 A**长**变量到该提供程序返回的当前操作所影响的记录数。  
  
> [!NOTE]
>  此参数仅返回操作; 所影响的记录的数它不从用于生成 select 语句返回的记录计数**记录集**。  
  
## <a name="remarks"></a>注释  
 使用**签名**方法以返回结果的复合命令语句中的下一步命令或存储过程返回多个结果。 如果你打开**记录集**复合命令语句上基于的对象 (例如，"选择\*从 table1;选择\*从 table2") 使用[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法[命令](../../../ado/reference/ado-api/command-object-ado.md)或[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**，ADO 执行仅第一个命令并返回到结果*记录集*。 若要访问的语句中的后续命令的结果，调用**签名**方法。  
  
 只要有更多结果和**记录集**包含复合语句未断开连接或跨进程边界封送**签名**方法将继续到返回**记录集**对象。 如果返回行的命令成功执行，但未返回任何记录，返回**记录集**对象将被打开，但为空。 通过验证，这种情况下的测试[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性均**True**。 如果非???返回行的命令执行成功，返回**记录集**对象将被关闭，你可以通过测试来验证其[状态](../../../ado/reference/ado-api/state-property-ado.md)属性**记录集**。 当没有更多结果，*记录集*将设置为*执行任何操作*。  
  
 **签名**方法上断开连接没有**记录集**对象，其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)已设置为**执行任何操作**(在 Microsoft Visual Basic) 或 NULL （在其他语言） 中。  
  
 如果正在处于立即更新模式下时进行了编辑，则调用**签名**方法将生成错误; 调用[更新](../../../ado/reference/ado-api/update-method.md)或[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一个。  
  
 若要在复合语句中传递多个命令的参数，通过填充[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合，或者通过将与原始数组**打开**或**执行**调用时，参数必须为集合或数组顺序命令序列中其相应命令相同。 你必须完成读取输出参数值之前读取所有结果。  
  
 OLE DB 访问接口确定复合语句中的每个命令执行的时间。 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，例如，在收到的复合语句批处理中执行所有命令。 生成**记录集**只需在调用时返回**签名**。  
  
 但是，其他提供程序可能执行的下一个命令在语句中只有调用签名之后。 对于这些提供程序，如果你显式关闭**记录集**对象在逐句通过整个命令语句中之前, ADO 永远不会执行剩余的命令。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [方法签名示例 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [方法签名的示例 （VC + +）](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   

