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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920927"
---
# <a name="ado-methods"></a>ADO 方法

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|创建可更新的新记录**记录集**对象。|  
|[追加](../../../ado/reference/ado-api/append-method-ado.md)|将对象追加到集合。 如果集合是**字段**，一个新**字段**追加到集合之前，可能会创建对象。|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|将数据追加到大文本或二进制数据**字段**，或设置为**参数**对象。|  
|[BeginTrans、 CommitTrans 和 RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|管理事务中处理**连接**对象，如下所示：<br /><br /> **BeginTrans** -开始新事务。<br /><br /> **CommitTrans** -保存任何更改并结束当前事务。 它还可能会启动新事务。<br /><br /> **RollbackTrans** -取消任何更改并结束当前事务。 它还可能会启动新事务。|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|取消执行的挂起异步方法调用。|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|取消挂起的批更新。|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|取消对当前或新行所做的任何更改**记录集**对象，或**字段**的集合**记录**对象，然后才能调用**更新**方法。|  
|[Clear](../../../ado/reference/ado-api/clear-method-ado.md)|移除所有**错误**中的对象**错误**集合。|  
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|创建重复**记录集**对象从现有**记录集**对象。 （可选） 指定的克隆是只读的。|  
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|关闭打开的对象和所有依赖对象。|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|比较两个书签，并返回其相对值的指示。|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|将文件或目录，并将其内容复制到另一个位置。|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|复制指定的数目的字符或字节 (具体取决于**类型**) 中**Stream**到另一个**Stream**对象。|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|创建一个新**参数**具有指定的属性的对象。|  
|[删除 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|删除从对象**参数**集合。|  
|[删除 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|删除从对象**字段**集合。|  
|[删除 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|删除当前记录或一组记录。|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|删除文件或目录，并将所有的子目录。|  
|[执行 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|执行查询、 SQL 语句或存储的过程中指定**CommandText**属性。|  
|[执行 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|执行指定的查询，SQL 语句、 存储的过程或特定于提供程序的文本。|  
|[查找](../../../ado/reference/ado-api/find-method-ado.md)|搜索**记录集**满足指定的条件的行。|  
|[刷新](../../../ado/reference/ado-api/flush-method-ado.md)|强制的内容**Stream** ADO 缓冲区使用的基础对象中的剩余**Stream**相关联。|  
|[get_OLEDBCommand 方法](../../../ado/reference/ado-api/get-oledbcommand-method.md)|返回基础 OLEDB 命令，首先传播到 OLEDB 命令在 ADO 命令上设置的任何参数信息。|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|返回**记录集**中的行表示的文件和表示此目录中的子目录**记录**。|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|返回所有或较大文本或二进制数据内容的一部分**字段**对象。|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|从 Shape 提供程序检索基础 OLEDB 数据源对象。|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|检索的多个记录**记录集**到一个数组对象。|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|返回**记录集**作为字符串。|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|加载到现有文件的内容**Stream**。|  
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|移动中的当前记录的位置**记录集**对象。|  
|[MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|将移动到 first、 last、 下一步，或上一个记录中指定**记录集**对象并将该记录的当前记录。|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|用于将文件或目录及其内容移动到另一个位置。|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|清除当前**记录集**对象并返回下一步**记录集**方法通过一系列命令。|  
|[打开 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)|将打开与数据源的连接。|  
|[打开 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)|此时将打开一个现有**记录**对象，或创建新文件或目录。|  
|[打开 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|将打开一个游标。|  
|[打开 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)|此时将打开**Stream**要操作的二进制或文本数据的流对象。|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|从提供程序获取数据库架构信息。|  
|[put_OLEDBCommand 方法](../../../ado/reference/ado-api/put-oledbcommand-method.md)|此方法会执行任何操作-它始终返回 S_OK。|  
|[读取](../../../ado/reference/ado-api/read-method.md)|读取指定的数量的字节从**Stream**对象。|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|从文本读取指定的数目的字符**Stream**对象。|  
|[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)|更新以反映，从可用对象的集合和特定于中的对象，提供程序。|  
|[再次查询](../../../ado/reference/ado-api/requery-method.md)|更新中的数据**记录集**通过重新执行的查询该对象所基于的对象。|  
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|刷新在当前数据**记录集**对象，或**字段**的集合**记录**对象，从基础数据库。|  
|[保存](../../../ado/reference/ado-api/save-method.md)|将保存**记录集**文件中或**Stream**对象。|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|将保存的二进制内容组成**Stream**到文件。|  
|[查找](../../../ado/reference/ado-api/seek-method.md)|搜索的索引**记录集**快速找到匹配指定的值，并将更改为该行的当前行位置的行。|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|设置流的末尾的位置。|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|读取文本流时，将跳过一个整行。|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|获取有关打开的流的统计信息。|  
|[支持](../../../ado/reference/ado-api/supports-method.md)|确定指定**记录集**对象支持特定类型的功能。|  
|[Update](../../../ado/reference/ado-api/update-method.md)|将保存到的当前行的任何更改**记录集**对象，或**字段**的集合**记录**对象。|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|将所有挂起的批更新写入到磁盘。|  
|[编写](../../../ado/reference/ado-api/write-method.md)|将二进制数据写入**Stream**对象。|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|将一个指定的文本字符串写入**Stream**对象。|  
  
## <a name="see-also"></a>请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 动态属性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 B：ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 对象和接口](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
