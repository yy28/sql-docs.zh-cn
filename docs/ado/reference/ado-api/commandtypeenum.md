---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 11150cb69914cf5438d46cc15238b38465ddfa30
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="commandtypeenum"></a>CommandTypeEnum
指定应如何解释命令自变量。  
  
 务必验证用户提供*CommandString*值以避免使应用程序用户有机会注入潜在的危险 ADO 执行的命令。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|未指定的命令类型自变量。|  
|**adCmdText**|1|计算结果[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)作为文本定义命令或存储的过程的调用。|  
|**adCmdTable**|2|计算结果**CommandText**为其列都由内部生成的 SQL 查询返回的表名。|  
|**adCmdStoredProc**|4|计算结果**CommandText**作为存储的过程名称。|  
|**adCmdUnknown**|8|默认值。 指示中的命令类型**CommandText**属性未知。<br /><br /> ADO 时不知道类型的命令，将经过多次尝试解释**CommandText**。<br /><br /> -   **CommandText**解释为命令或存储过程调用的文本定义。 这是相同的行为**adCmdText**。<br />-   **CommandText**是存储过程的名称。 这是相同的行为**adCmdStoredProc**。<br />-   **CommandText**解释为表的名称。 所有列都由内部生成的 SQL 查询都返回。 这是相同的行为**adCmdTable**。|  
|**adCmdFile**|256|计算结果**CommandText**作为永久存储的文件名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 与使用**记录集。**[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)或[Requery](../../../ado/reference/ado-api/requery-method.md)仅。|  
|**adCmdTableDirect**|512|计算结果**CommandText**为所有返回其列的表名。 与使用**Recordset.Open**或**Requery**仅。 若要使用[Seek](../../../ado/reference/ado-api/seek-method.md)方法，**记录集**必须使用打开**adCmdTableDirect**。<br /><br /> 此值不能与组合[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值**adAsyncExecute**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package: **com.ms.wfc.data**  
  
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
