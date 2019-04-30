---
title: NextRecordset 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fba1826dcad9a183bab9b9b0106bb9b45eb29846
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242428"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset 方法 (ADO)
清除当前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象并返回下一步**记录集**方法通过一系列命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>返回值  
 返回**记录集**对象。 在语法模型中， *recordset1*并*recordset2*可以是相同的**记录集**对象，也可以使用单独的对象。 当使用单独**记录集**对象，重置**ActiveConnection**属性上原始**记录集**(*recordset1*)后**NextRecordset**已调用将生成错误。  
  
#### <a name="parameters"></a>Parameters  
 *RecordsAffected*  
 可选。 一个**长**变量向其提供程序返回的当前操作所影响的记录数。  
  
> [!NOTE]
>  此参数仅返回受影响的操作; 记录数它不会从用于生成的 select 语句返回的记录数**记录集**。  
  
## <a name="remarks"></a>备注  
 使用**NextRecordset**方法以返回结果的复合命令语句中的下一个命令或存储过程返回多个结果。 如果您打开**记录集**对象，基于复合命令语句 (例如，"选择\*从 table1;选择\*table2 从") 使用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法[命令](../../../ado/reference/ado-api/command-object-ado.md)或[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**，ADO 执行仅第一个命令并返回到结果*记录集*。 若要访问的语句中的后续命令的结果，请调用**NextRecordset**方法。  
  
 只要有更多结果，**记录集**包含复合语句未断开连接或跨进程边界封送**NextRecordset**方法仍将继续到返回**记录集**对象。 如果返回行的命令成功执行，但未返回任何记录，返回**记录集**对象将被打开，但为空。 只需验证这种情况下的测试[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)并[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)两个属性均**True**。 如果不返回行的命令执行成功，返回**记录集**对象将被关闭，您可以通过测试来验证这[状态](../../../ado/reference/ado-api/state-property-ado.md)属性上的**记录集**. 当没有更多结果*记录集*将设置为*Nothing*。  
  
 **NextRecordset**方法不是可在上找到已断开连接**记录集**对象，其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)已设置为**Nothing**(Microsoft Visual Basic 中) 或 NULL （在其他语言）。  
  
 如果编辑正在进行中立即更新模式中，则调用**NextRecordset**方法将生成错误; 调用[更新](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一个。  
  
 在复合语句中，将多个命令的参数传递的填充[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合，或通过传递原始数组**打开**或**Execute**调用时，参数必须在集合或数组中顺序中的命令系列及其各自的命令相同。 必须完成读取输出参数值之前读取所有结果。  
  
 OLE DB 访问接口确定复合语句中的每个命令执行时。 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，例如，在收到的复合语句批处理中执行的所有命令。 得到**记录集**只需返回在调用时**NextRecordset**。  
  
 但是，其他提供程序可能执行下一个命令在语句中只能调用 NextRecordset 后。 对于这些提供程序，如果您显式关闭**记录集**ADO 永远不会执行剩余的命令之前通过整个命令语句中，单步执行对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [NextRecordset 方法示例 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset 方法示例 (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
