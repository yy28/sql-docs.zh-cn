---
title: "ExecuteOptionEnum |Microsoft 文档"
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
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74248756628e892ff8a00e0e6e206b5eb7639e05
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
指定如何提供程序应执行的命令。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|指示应以异步方式执行该命令。<br /><br /> 此值不能与组合[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。|  
|**adAsyncFetch**|0x20|指示的剩余行中指定的初始数量后[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)应以异步方式检索属性。|  
|**adAsyncFetchNonBlocking**|0x40|指示检索时永远不会阻止主线程。 如果检索不到请求的行，当前行自动移动到文件末尾。<br /><br /> 如果你打开[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从[流](../../../ado/reference/ado-api/stream-object-ado.md)包含永久存储**记录集**， **adAsyncFetchNonBlocking**不会一种效果;该操作将同步和阻塞。<br /><br /> **adAsynchFetchNonBlocking**没有时生效[adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)选项用于打开**记录集**。|  
|**adExecuteNoRecords**|0x80|指示命令文本的命令或存储的过程不会返回行 （例如，仅将数据插入命令）。 如果检索任何行时，它们是放弃，并且不返回。<br /><br /> **adExecuteNoRecords**只能为可选参数的形式传递**命令**或**连接执行**方法。|  
|**adExecuteStream**|0x400|指示应以流的形式返回的命令执行的结果。<br /><br /> **adExecuteStream**只能为可选参数的形式传递**命令执行**方法。|  
|**adExecuteRecord**||指示**CommandText**是命令或存储的过程返回单个行应返回为**记录**对象。|  
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
|[执行方法 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|[执行方法 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery 方法](../../../ado/reference/ado-api/requery-method.md)|

