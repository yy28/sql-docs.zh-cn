---
title: ExecuteOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bef70bd72425e749865e31ecf162e719737dd272
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932848"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
指定如何提供程序应执行的命令。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|指示应以异步方式执行该命令。<br /><br /> 此值不能合并在一起[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。|  
|**adAsyncFetch**|0x20|指示的各行中指定的初始数量后[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)应以异步方式检索属性。|  
|**adAsyncFetchNonBlocking**|0x40|指示检索时永远不会阻止主线程。 如果检索不到请求的行，当前行自动移动到文件末尾。<br /><br /> 如果您打开[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从[Stream](../../../ado/reference/ado-api/stream-object-ado.md)包含永久存储**记录集**， **adAsyncFetchNonBlocking**不会一种效果;该操作将同步和正在阻塞。<br /><br /> **adAsynchFetchNonBlocking**没有时生效[adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)选项用于打开**记录集**。|  
|**adExecuteNoRecords**|0x80|指示命令文本的命令或存储的过程不返回行 （例如，仅将数据插入的命令）。 如果检索不到任何行，它们被丢弃而不会返回。<br /><br /> **adExecuteNoRecords**只能为可选参数的形式传递**命令**或**连接执行**方法。|  
|**adExecuteStream**|0x400|指示应以流的形式返回的命令执行的结果。<br /><br /> **adExecuteStream**只能为可选参数的形式传递**Command Execute**方法。|  
|**adExecuteRecord**||指示**CommandText**是命令或返回单个行，其中应作为返回的存储的过程**记录**对象。|  
|**adOptionUnspecified**|-1|指示该命令未指定。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Execute 方法（ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute 方法（ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery 方法](../../../ado/reference/ado-api/requery-method.md)|
