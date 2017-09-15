---
title: "ADO 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ffd5c3c3a735c86aa39f7ab0b521bb23e0c4e14
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="ado-methods"></a>ADO 方法
|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|创建可更新的新记录**记录集**对象。|  
|[追加](../../../ado/reference/ado-api/append-method-ado.md)|将对象追加到集合。 如果该集合为**字段**，新**字段**追加到集合之前，可能会创建对象。|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|将数据追加到较大文本或二进制数据**字段**，或**参数**对象。|  
|[BeginTrans、 CommitTrans 和不](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|管理在内部处理的事务**连接**对象，如下所示：<br /><br /> **BeginTrans** -开始新事务。<br /><br /> **CommitTrans** -保存任何更改并结束当前事务。 它还可能会启动一个新的事务。<br /><br /> **如果不**-取消任何更改并结束当前事务。 它还可能会启动一个新的事务。|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|取消执行的挂起异步方法调用。|  
|[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|取消挂起的批更新。|  
|[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|取消对的当前或新行所做的任何更改**记录集**对象，或**字段**集合**记录**对象，然后再调用**更新**方法。|  
|[Clear](../../../ado/reference/ado-api/clear-method-ado.md)|中删除所有**错误**对象从**错误**集合。|  
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|创建副本**记录集**从现有对象**记录集**对象。 （可选） 指定的克隆是只读的。|  
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|关闭打开的对象和任何从属对象。|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|比较两个的书签，并返回对其相对值的指示。|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|将文件或目录，并将其内容复制到另一个位置。|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|将复制指定的字符或字节数 (具体取决于**类型**) 中**流**到另一个**流**对象。|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|创建一个新**参数**具有指定的属性的对象。|  
|[删除 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|删除从对象**参数**集合。|  
|[删除 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|删除从对象**字段**集合。|  
|[删除 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|删除当前记录或一组记录。|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|删除文件或目录，并将其所有子目录。|  
|[执行 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)|执行查询、 SQL 语句或存储的过程中指定**CommandText**属性。|  
|[执行 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)|执行指定的查询、 SQL 语句、 存储的过程或提供程序特定的文本。|  
|[查找](../../../ado/reference/ado-api/find-method-ado.md)|搜索**记录集**满足指定的条件的行。|  
|[刷新](../../../ado/reference/ado-api/flush-method-ado.md)|强制的内容**流**与其的基础对象的 ADO 缓冲区中剩余**流**关联。|  
|[get_OLEDBCommand 方法](../../../ado/reference/ado-api/get-oledbcommand-method.md)|返回基础 OLEDB 命令，首先将传播到 OLEDB 命令在 ADO 命令上设置任何参数信息。|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|返回**记录集**其行表示的文件和表示此目录中的子目录**记录**。|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|返回所有或较大文本或二进制数据的内容的一部分**字段**对象。|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|从 Shape 提供程序检索基础的 OLEDB 数据源对象。|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|检索的多个记录**记录集**到一个数组对象。|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|返回**记录集**作为字符串。|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|加载到现有文件的内容**流**。|  
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|移动中的当前记录的位置**记录集**对象。|  
|[MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|将移动到第一个，最后，在指定的下一步，或上一个记录**记录集**对象并将该记录的当前记录。|  
|[移动记录](../../../ado/reference/ado-api/moverecord-method-ado.md)|用于将文件或目录及其内容移到另一个位置。|  
|[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|清除当前**记录集**对象并返回下一个**记录集**方法通过一系列的命令。|  
|[打开 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)|打开与数据源的连接。|  
|[打开 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)|打开现有**记录**对象，或创建新文件或目录。|  
|[打开 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|打开一个游标。|  
|[打开 （ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)|打开**流**对象操作的二进制或文本数据的流。|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|从提供程序获取数据库架构信息。|  
|[put_OLEDBCommand 方法](../../../ado/reference/ado-api/put-oledbcommand-method.md)|此方法不执行任何操作-它始终返回，则为 S_OK。|  
|[读取](../../../ado/reference/ado-api/read-method.md)|读取指定的数目的字节从**流**对象。|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|从文本文件中读取指定的数目的字符**流**对象。|  
|[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)|更新以反映，从可用的对象的集合和特定中的对象，提供程序。|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|更新中的数据**记录集**通过重新执行的查询所基于的对象的对象。|  
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|刷新当前中的数据**记录集**对象，或**字段**集合**记录**对象，从基础数据库。|  
|[保存](../../../ado/reference/ado-api/save-method.md)|将保存**记录集**文件中或**流**对象。|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|将保存的二进制内容组成**流**到文件。|  
|[查找](../../../ado/reference/ado-api/seek-method.md)|搜索的索引**记录集**快速找到的行与匹配的指定的值，并更改为该行的当前行位置。|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|设置为流的末尾的位置。|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|在读取文本流时，将跳过一整行。|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|获取有关打开的流的统计信息。|  
|[支持](../../../ado/reference/ado-api/supports-method.md)|确定指定**记录集**对象支持特定类型的功能。|  
|[Update](../../../ado/reference/ado-api/update-method.md)|将保存的当前行的任何更改**记录集**对象，或**字段**集合**记录**对象。|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|将写入磁盘的所有挂起的批更新。|  
|[写入](../../../ado/reference/ado-api/write-method.md)|写入二进制数据保存到**流**对象。|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|将一个指定的文本字符串写入**流**对象。|  
  
## <a name="see-also"></a>另请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 动态属性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 枚举常量](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附录 b: ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 对象模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 对象和接口](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 属性](../../../ado/reference/ado-api/ado-properties.md)
