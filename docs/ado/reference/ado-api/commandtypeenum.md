---
title: CommandTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 09874df6d9e09da8b6dc0df3e9670e4ff130c511
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695976"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
指定应如何解释命令参数。  
  
 务必要验证用户提供*CommandString*值以避免让应用程序用户有机会来插入具有潜在危险 ADO 执行的命令。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|不会指定命令类型参数。|  
|**adCmdText**|1|计算结果[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)作为文本定义的命令或存储的过程的调用。|  
|**adCmdTable**|2|计算结果**CommandText**为其列都由内部生成的 SQL 查询返回的表名。|  
|**adCmdStoredProc**|4|计算结果**CommandText**作为存储的过程名称。|  
|**adCmdUnknown**|8|默认值。 指示命令中的类型**CommandText**属性未知。<br /><br /> ADO 时的命令的类型未知，将经过多次尝试解释**CommandText**。<br /><br /> -   **CommandText**被解释为文本的命令或存储过程调用的定义。 这是相同的行为**adCmdText**。<br />-   **CommandText**是存储过程的名称。 这是相同的行为**adCmdStoredProc**。<br />-   **CommandText**被解释为表的名称。 通过在内部生成的 SQL 查询返回所有列。 这是相同的行为**adCmdTable**。|  
|**adCmdFile**|256|计算结果**CommandText**作为永久存储的文件名[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 用于**记录集。** [开放](../../../ado/reference/ado-api/open-method-ado-recordset.md)或[再次查询](../../../ado/reference/ado-api/requery-method.md)仅。|  
|**adCmdTableDirect**|512|计算结果**CommandText**为所有返回其列的表名。 用于**Recordset.Open**或**再次查询**仅。 若要使用[Seek](../../../ado/reference/ado-api/seek-method.md)方法，**记录集**必须使用打开**adCmdTableDirect**。<br /><br /> 此值不能合并在一起[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值**adAsyncExecute**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[CommandType 属性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Execute 方法（ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute 方法（ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery 方法](../../../ado/reference/ado-api/requery-method.md)||
