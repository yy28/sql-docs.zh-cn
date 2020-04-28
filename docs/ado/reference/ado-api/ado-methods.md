---
title: ADO 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8df204daeda82f809cf50246590141729e3608e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920927"
---
# <a name="ado-methods"></a>ADO 方法

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|为可更新的**记录集**对象创建新记录。|  
|[附加](../../../ado/reference/ado-api/append-method-ado.md)|将对象追加到集合。 如果集合是**字段**，则可以在将其追加到集合之前创建新的**字段**对象。|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|将数据追加到大文本或二进制数据**字段**，或追加到**参数**对象。|  
|[BeginTrans、CommitTrans 和 RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|管理**连接**对象中的事务处理，如下所示：<br /><br /> **BeginTrans** -开始新的事务。<br /><br /> **CommitTrans** -保存所有更改并结束当前事务。 它还可能会启动新的事务。<br /><br /> **RollbackTrans** -取消所有更改并结束当前事务。 它还可能会启动新的事务。|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|取消执行挂起的异步方法调用。|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|取消挂起的批更新。|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|在调用**Update**方法之前，取消对**Recordset**对象的当前行或新行所做的任何更改，或**记录**对象的**字段**集合。|  
|[清除](../../../ado/reference/ado-api/clear-method-ado.md)|从**错误**集合中移除所有**错误**对象。|  
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|从现有**记录集**对象创建重复的**记录集**对象。 还可以指定克隆为只读。|  
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|关闭打开的对象和所有依赖对象。|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|比较两个书签，并返回其相对值的指示值。|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|将文件或目录及其内容复制到其他位置。|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|将**流**中指定数量的字符或字节（取决于**类型**）复制到另一个**流**对象。|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|创建一个具有指定属性的新**参数**对象。|  
|[Delete （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|从**参数**集合中删除对象。|  
|[删除（ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|从 "**字段**" 集合中删除一个对象。|  
|[删除（ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|删除当前记录或一组记录。|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|删除文件或目录及其所有子目录。|  
|[Execute （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|执行在**CommandText**属性中指定的查询、SQL 语句或存储过程。|  
|[Execute （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|执行指定的查询、SQL 语句、存储过程或特定于提供程序的文本。|  
|[查找](../../../ado/reference/ado-api/find-method-ado.md)|在**记录集中**搜索满足指定条件的行。|  
|[平](../../../ado/reference/ado-api/flush-method-ado.md)|将 ADO 缓冲区中的**流**的内容强制转换为与**流**关联的基础对象。|  
|[get_OLEDBCommand 方法](../../../ado/reference/ado-api/get-oledbcommand-method.md)|返回基础 OLEDB 命令，首先将在 ADO 命令上设置的所有参数信息传播到 OLEDB 命令。|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|返回一个**记录集**，其行表示此**记录**所表示的目录中的文件和子目录。|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|返回大文本或二进制数据**字段**对象的全部或部分内容。|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|从形状提供程序中检索基础 OLEDB 数据源对象。|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|将**记录集**对象的多个记录检索到一个数组中。|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|以字符串的形式返回**记录集**。|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|将现有文件的内容加载到**流**中。|  
|[移动](../../../ado/reference/ado-api/move-method-ado.md)|移动**记录集**对象中的当前记录的位置。|  
|[MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|移动到指定**记录集**对象中的第一条、最后一条、下一条记录或上一条记录，并使该记录成为当前记录。|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|将文件或目录及其内容移到其他位置。|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|清除当前**记录集**对象，并通过前进一系列命令来返回下一个**记录集**。|  
|[打开（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)|打开与数据源的连接。|  
|[打开（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)|打开现有**记录**对象，或创建新的文件或目录。|  
|[Open （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|打开游标。|  
|[打开（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)|打开一个**流**对象以处理二进制或文本数据的流。|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|从提供程序中获取数据库架构信息。|  
|[put_OLEDBCommand 方法](../../../ado/reference/ado-api/put-oledbcommand-method.md)|此方法不执行任何操作-始终返回 S_OK。|  
|[读取](../../../ado/reference/ado-api/read-method.md)|从**流**对象中读取指定数目的字节。|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|从文本**流**对象中读取指定数目的字符。|  
|[全部](../../../ado/reference/ado-api/refresh-method-ado.md)|更新集合中的对象，以反映提供程序提供的和特定于提供程序的对象。|  
|[重新](../../../ado/reference/ado-api/requery-method.md)|通过重新执行对象所基于的查询来更新**记录集**对象中的数据。|  
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|刷新当前**记录集**对象中的数据，或从基础数据库刷新**记录**对象的**字段**集合中的数据。|  
|[保存](../../../ado/reference/ado-api/save-method.md)|将**记录集**保存到文件或**流**对象中。|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|将**流**的二进制内容保存到文件。|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|搜索**记录集**的索引以快速找到与指定值匹配的行，并将当前行的位置更改为该行。|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|设置流的结束位置。|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|读取文本流时，跳过整行。|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|获取有关打开的流的统计信息。|  
|[支持](../../../ado/reference/ado-api/supports-method.md)|确定指定的**记录集**对象是否支持特定类型的功能。|  
|[Update](../../../ado/reference/ado-api/update-method.md)|保存对记录**集**对象的当前行所做的任何更改，或**记录**对象的**字段**集合。|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|将所有挂起的批更新写入磁盘。|  
|[写入](../../../ado/reference/ado-api/write-method.md)|向**Stream**对象写入二进制数据。|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|向**Stream**对象写入指定的文本字符串。|  
  
## <a name="see-also"></a>另请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 动态属性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 B： ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 对象和接口](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
