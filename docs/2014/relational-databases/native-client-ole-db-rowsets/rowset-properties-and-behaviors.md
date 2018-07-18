---
title: 行集属性和行为 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], properties
- SQL Server Native Client OLE DB provider, rowsets
- properties [OLE DB]
- OLE DB rowsets, properties
ms.assetid: 9baabcb6-0114-42f2-89f8-d8d66b3c8c14
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e4f42510189dacefd060450cec5e56d986b7c322
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423586"
---
# <a name="rowset-properties-and-behaviors"></a>行集属性和行为
  这些是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口行集属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_ABORTPRESERVE|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：行集在某个中止操作后的行为由此属性确定。<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使行集失效后中止操作。 行集对象的功能几乎丢失。 仅支持**IUnknown**操作以及释放未完成的行和取值函数句柄。<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序保持有效的行集。|  
|DBPROP_ACCESSORDER|R/w： 读/写<br /><br /> 默认值：DBPROPVAL_AO_RANDOM<br /><br /> 说明：访问顺序。 访问行集中的列时必须遵照的顺序。<br /><br /> DBPROPVAL_AO_RANDOM：可以按任意顺序访问列。<br /><br /> DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS：只能按照由列序号确定的顺序依次访问绑定为存储对象的列。<br /><br /> DBPROPVAL_AO_SEQUENTIAL：所有列都必须按照由列序号确定的顺序依次访问。|  
|DBPROP_APPENDONLY|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|R/w： 只读<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口存储对象阻止使用其他行集方法。|  
|DBPROP_BOOKMARKS DBPROP_LITERALBOOKMARKS|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口行集行标识为 DBPROP_BOOKMARKS 或 DBPROP_LITERALBOOKMARKS 为 VARIANT_TRUE 时，支持书签。<br /><br /> 将其中任一属性设置为 VARIANT_TRUE 都不会启用按书签为行集定位。 将 DBPROP_IRowsetLocate 或 DBPROP_IRowsetScroll 设置为 VARIANT_TRUE 可创建支持按书签为行集定位的行集。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标以支持包含书签的行集。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。 **注意：** 设置这些属性与其他冲突[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口游标定义的属性将导致错误。 例如，如果将 DBPROP_BOOKMARKS 设置为 VARIANT_TRUE 且 DBPROP_OTHERINSERT 也为 VARIANT_TRUE，那么，当使用者尝试打开行集时，将生成错误。|  
|DBPROP_BOOKMARKSKIPPED|R/w： 只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口返回 DB_E_BADBOOKMARK，如果使用者指示某个无效的书签时定位或搜索标有书签的行集。|  
|DBPROP_BOOKMARKTYPE|R/w： 只读<br /><br /> 默认值：DBPROPVAL_BMK_NUMERIC<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口只实现数字书签。 一个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口书签为 32 位无符号的整数，类型为 DBTYPE_UI4。|  
|DBPROP_CACHEDEFERRED|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_CANFETCHBACKWARDS DBPROP_CANSCROLLBACKWARDS|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持向后提取和滚动中非序列行集中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当 DBPROP_CANFETCHBACKWARDS 或 DBPROP_CANSCROLLBACKWARDS 为 VARIANT_TRUE 时，Native Client OLE DB 访问接口创建游标支持行集。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。|  
|DBPROP_CANHOLDROWS|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将返回 DB_E_ROWSNOTRELEASED 如果使用者试图获得多个行的挂起的更改的行集时存在这些当前行集。 可以修改此行为。<br /><br /> 将 DBPROP_CANHOLDROWS 和 DBPROP_IRowsetChange 同时设置为 VARIANT_TRUE 意味着行集带有书签。 如果这两个属性均为 VARIANT_TRUE， **IRowsetLocate**上行集提供接口，并且 DBPROP_BOOKMARKS 和 DBPROP_LITERALBOOKMARKS 均为 VARIANT_TRUE。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口行集包含书签的受[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标。|  
|DBPROP_CHANGEINSERTEDROWS|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：如果行集正在使用由键集驱动的游标，则此属性只能设置为 VARIANT_TRUE。|  
|DBPROP_COLUMNRESTRICT|R/w： 只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序时将属性设置为 variant_true，则使用者不能更改行集中的列。 可以更新行集中的其他列，并且可以删除行本身。<br /><br /> 如果该属性为 VARIANT_TRUE，使用者将检查*dwFlags* DBCOLUMNINFO 结构的成员，才能确定是否可以写入单独列的值。 对于可修改的列， *dwFlags*展现 DBCOLUMNFLAGS_WRITE。|  
|DBPROP_COMMANDTIMEOUT|R/w： 读/写<br /><br /> 默认值： 0<br /><br /> 说明： 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序上不会超时**icommand:: Execute**方法。|  
|DBPROP_COMMITPRESERVE|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：行集在某个提交操作后的行为由此属性确定。<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序保持有效的行集。<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使行集失效之后的提交操作。 行集对象的功能几乎丢失。 仅支持**IUnknown**操作以及释放未完成的行和取值函数句柄。|  
|DBPROP_DEFERRED|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 当设置为 VARIANT_TRUE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将尝试使用服务器游标用于行集。 **文本**， **ntext**，和**图像**列从服务器不会进行返回，直到应用程序访问它们。|  
|DBPROP_DELAYSTORAGEOBJECTS|R/w： 只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口存储对象上支持立即更新模式。<br /><br /> 对连续流对象中的数据所做的更改将立即提交到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 将基于行集事务模式提交修改。|  
|DBPROP_HIDDENCOLUMNS|R/w： 只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> **说明：** 隐藏列计数<br /><br /> 如果 DBPROP_UNIQUEROWS 为 VARIANT_TRUE，则 DBPROP_HIDDENCOLUMNS 属性返回由访问接口添加的唯一标识行集中各行的其他“隐藏”列的数量。 这些列返回的**icolumnsinfo:: Getcolumninfo**并**icolumnsrowset:: Getcolumnsrowset**。 但是，它们不包括在返回的行数*pcColumns*返回的参数**icolumnsinfo:: Getcolumninfo**。<br /><br /> 若要确定列中表示总数*prgInfo*由返回结构**icolumnsinfo:: Getcolumninfo**，包括隐藏列，使用者将 DBPROP_ 的值从返回的列计数的 HIDDENCOLUMNS **icolumnsinfo:: Getcolumninfo**中*pcColumns*。 如果 DBPROP_UNIQUEROWS 为 VARIANT_FALSE，则 DBPROP_HIDDENCOLUMNS 为零。|  
|DBPROP_IAccessor DBPROP_IColumnsInfo DBPROP_IConvertType DBPROP_IRowset DBPROP_IRowsetInfo|R/w： 只读<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持这些接口上的所有行集。|  
|DBPROP_IColumnsRowset|R/w： 读/写<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持**IColumnsRowset**接口。|  
|DBPROP_IConnectionPointContainer|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：IConnectionPointContainer。 如果为 VARIANT_TRUE，则行集支持指定的接口。 如果为 VARIANT_FALSE，则行集不支持指定的接口。 支持某接口的访问接口必须支持与该接口关联的且值为 VARIANT_TRUE 的属性。 这些属性主要用于通过 ICommandProperties::SetProperties 请求接口。|  
|DBPROP_IMultipleResults|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持**IMultipleResults**接口。|  
|DBPROP_IRowsetChange DBPROP_IRowsetUpdate|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持**IRowsetChange**并**IRowsetUpdate**接口。<br /><br /> 通过使用 DBPROP_IRowsetChange 等于 VARIANT_TRUE 而创建的行集将展现立即更新模式行为。<br /><br /> 当 DBPROP_IRowsetUpdate 为 VARIANT_TRUE 时，DBPROP_IRowsetChange 也为 VARIANT_TRUE。 行集展现延迟的更新模式行为。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标以支持行集公开任一**IRowsetChange**或**IRowsetUpdate**。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。|  
|DBPROP_IRowsetIdentity|R/w： 读/写<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持**IRowsetIdentity**接口。 如果行集支持此接口，则任何表示同一基础行的两个句柄将始终反映相同的数据和状态。 使用者可以调用**IRowsetIdentity:: IsSameRow**方法来比较两个行句柄，以查看它们是否引用同一个行实例。|  
|DBPROP_IRowsetLocate DBPROP_IRowsetScroll|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口可以显示**IRowsetLocate**并**IRowsetScroll**接口。<br /><br /> 当 DBPROP_IRowsetLocate 为 VARIANT_TRUE 时，DBPROP_CANFETCHBACKWARDS 和 DBPROP_CANSCROLLBACKWARDS 也为 VARIANT_TRUE。<br /><br /> 当 DBPROP_IRowsetScroll 为 VARIANT_TRUE 时，DBPROP_IRowsetLocate 也为 VARIANT_TRUE，并且这两个接口可用于行集。<br /><br /> 每个接口都要求书签。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口设置 DBPROP_BOOKMARKS 和 DBPROP_LITERALBOOKMARKS 为 VARIANT_TRUE 时使用者请求任一接口。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标以支持**IRowsetLocate**并**IRowsetScroll**。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。<br /><br /> 设置这些属性与其他冲突[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口游标定义的属性将导致错误。 例如，如果将 DBPROP_IRowsetScroll 设置为 VARIANT_TRUE（此时，DBPROP_OTHERINSERT 也为 VARIANT_TRUE），当使用者尝试打开行集时，将生成错误。|  
|DBPROP_IRowsetResynch|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**IRowsetResynch**按需的接口。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口可以显示任何行集上的接口。|  
|DBPROP_ISupportErrorInfo|R/w： 读/写<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**ISupportErrorInfo**行集上的接口。|  
|DBPROP_ILockBytes|此接口未实现通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入此属性将生成错误。|  
|DBPROP_ISequentialStream|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**ISequentialStream**接口以支持长时间，长度可变的数据存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|DBPROP_IStorage|此接口未实现通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入此属性将生成错误。|  
|DBPROP_IStream|此接口未实现通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入此属性将生成错误。|  
|DBPROP_IMMOBILEROWS|R/w： 读/写<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：此属性仅对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 键集游标为 VARIANT_TRUE；对于所有其他游标，它为 VARIANT_FALSE。<br /><br /> VARIANT_TRUE：行集将不对插入或更新的行重新排序。 有关**irowsetchange:: Insertrow**，行将出现在行集结尾。 有关**irowsetchange:: Setdata**，如果行集未排序，不会更改已更新的行的位置。 如果行集排序并**irowsetchange:: Setdata**更改用于排序的行集，该行的列不是移动。 如果行集建立在一组键列之上（通常是 DBPROP_OTHERUPDATEDELETE 为 VARIANT_TRUE 但 DBPROP_OTHERINSERT 为 VARIANT_FALSE 的行集），则更改某个键列的值通常等效于删除当前行并插入新行。 因此，如果 DBPROP_OWNINSERT 为 VARIANT_FALSE，则行可能从行集中移动，或甚至消失，即使 DBPROP_IMMOBILEROWS 属性为 VARIANT_TRUE，也不例外。<br /><br /> VARIANT_FALSE：如果对行集排序，则插入的行将以行集的正确顺序出现。 如果未对行集排序，则插入的行将出现在末尾。 如果**irowsetchange:: Setdata**使用的列更改为移动的行集，该行的顺序。 如果未对行集排序，则不更改行的位置。|  
|DBPROP_LITERALIDENTITY|R/w： 只读<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：此属性始终为 VARIANT_TRUE。|  
|DBPROP_LOCKMODE|R/w： 读/写<br /><br /> 默认值：DBPROPVAL_LM_NONE<br /><br /> 说明：由行集执行的锁定级别（DBPROPVAL_LM_NONE、DBPROPVAL_LM_SINGLEROW）。 **注意：** 时在事务中，使用快照隔离，如果通过使用键集游标或动态服务器游标打开行集并且锁定模式设置为 DBPROPVAL_LM_SINGLEROW，如果其他人已更新自该行提取行时将会出错启动事务。 对于其他游标类型和锁定模式，如果在自启动此事务之后其他人已更新了该行，则在该用户尝试更新此行之前，不会发生错误。 在这两种情况下，服务器将生成这些错误。|  
|DBPROP_MAXOPENROWS|R/w： 只读<br /><br /> 默认值： 0<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口不限制可以在行集中处于活动状态的行数。|  
|DBPROP_MAXPENDINGROWS|R/w： 只读<br /><br /> 默认值： 0<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口不限制与挂起的更改的行集行数。|  
|DBPROP_MAXROWS|R/w： 读/写<br /><br /> 默认值： 0<br /><br /> 说明： 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口不限制行集中的行数。 当使用者设置 dbprop_maxrows 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用 SET ROWCOUNT 语句限制行集中的行数。<br /><br /> SET ROWCOUNT 可能在执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句的过程中导致意外后果。 有关详细信息，请参阅[SET ROWCOUNT](/sql/t-sql/statements/set-rowcount-transact-sql)。|  
|DBPROP_MAYWRITECOLUMN|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_MEMORYUSAGE|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_NOTIFICATIONGRANULARITY|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_NOTIFICATIONPHASES|R/w： 只读<br /><br /> 默认值： DBPROPVAL_NP_OKTODO &#124; DBPROPVAL_NP_ABOUTTODO &#124; DBPROPVAL_NP_SYNCHAFTER &#124; DBPROPVAL_NP_FAILEDTODO &#124; DBPROPVAL_NP_DIDEVENT<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持所有通知阶段。|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|R/w： 只读<br /><br /> 默认值： DBPROPVAL_NP_OKTODO &#124; DBPROPVAL_NP_ABOUTTODO<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口通知阶段是取消之前尝试执行行集修改所指示。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持取消阶段后，尝试已完成。|  
|DBPROP_ORDEREDBOOKMARKS|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE DBPROP_OWNINSERT DBPROP_OWNUPDATEDELETE|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 设置更改可见性属性会导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标以支持行集。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。|  
|DBPROP_QUICKRESTART|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 当设置为 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将尝试使用服务器游标用于行集。|  
|DBPROP_REENTRANTEVENTS|R/w： 只读<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口行集是可重入，如果使用者尝试从通知回调访问属于入行行集的方法可能返回 DB_E_NOTREENTRANT。|  
|DBPROP_REMOVEDELETED|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序来更改基于对更改的可见性属性的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由行集公开的数据。<br /><br /> VARIANT_TRUE：当刷新行集时，将从行集中删除由使用者或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户删除的行。 DBPROP_OTHERINSERT 为 VARIANT_TRUE。<br /><br /> VARIANT_FALSE：当刷新行集时，将不从行集中删除由使用者或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户删除的行。 行集中已删除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 行的行状态值为 DBROWSTATUS_E_DELETED。 DBPROP_OTHERINSERT 为 VARIANT_TRUE。<br /><br /> 此属性仅对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标支持的行集具有值。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。<br /><br /> 由键集游标行集实现 DBPROP_REMOVEDELETED 属性时，在提取时删除了已删除的行，并且可能的行提取方法，如**GetNextRows**和**GetRowsAt，** 返回 S_OK 和比请求更少的行。 请注意，此行为并不指示 DB_S_ENDOFROWSET 条件，并且如果存在任何剩余的行，则返回的行数将从不会为零。|  
|DBPROP_REPORTMULTIPLECHANGES|由不实现此行集属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 尝试读取或写入属性值将生成错误。|  
|DBPROP_RETURNPENDINGINSERTS|R/w： 只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 提取行的方法调用时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不返回挂起的插入行。|  
|DBPROP_ROWRESTRICT|R/w： 只读<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口行集不支持基于行的访问权限。 如果**IRowsetChange**接口会在行集上公开**SetData**可以由使用者调用方法。|  
|DBPROP_ROWSET_ASYNCH|R/w： 读/写<br /><br /> 默认值： 0<br /><br /> 说明：为异步行集处理而提供。 此属性位于行集属性组和 DBPROPSET_ROWSET 属性集中。 类型为 VT_14。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 支持的位掩码中的唯一值是 `DBPROPVAL_ASYNCH_INITIALIZE`。|  
|DBPROP_ROWTHREADMODEL|R/w： 只读<br /><br /> 默认值：DBPROPVAL_RT_FREETHREAD<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口从单个使用者的多个执行线程对其对象支持访问。|  
|DBPROP_SERVERCURSOR|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：设置后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标将用于支持行集。 有关详细信息，请参阅[行集和 SQL Server 游标](rowsets-and-sql-server-cursors.md)。|  
|DBPROP_SERVERDATAONINSERT|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：插入的服务器数据。<br /><br /> VARIANT_TRUE：在将插入传输到服务器时，访问接口将从服务器检索数据以更新本地行缓存。<br /><br /> VARIANT_FALSE：访问接口不针对新插入的行检索服务器值。|  
|DBPROP_STRONGIDENTITY|R/w： 只读<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：强的行标识。 如果行集允许插入 (任一**IRowsetChange**或**IRowsetUpdate**为 true)，并且 DBPROP_UPDATABILITY 设置为支持 InsertRows，则 DBPROP_STRONGIDENTITY 的值取决于 DBPROP_CHANGEINSERTEDROWS 属性 （将 VARIANT_FALSE 如果 DBPROP_CHANGEINSERTEDROWS 属性值为 VARIANT_FALSE）。|  
|DBPROP_TRANSACTEDOBJECT|R/w： 只读<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口只支持事务的对象。 有关详细信息，请参阅[事务](../native-client-ole-db-transactions/transactions.md)。|  
|DBPROP_UNIQUEROWS|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：唯一行。<br /><br /> VARIANT_TRUE：每行由其列值唯一标识。 一组唯一标识行的列具有从返回的 DBCOLUMNINFO 结构中设置了 DBCOLUMNFLAGS_KEYCOLUMN **GetColumnInfo**方法。<br /><br /> VARIANT_FALSE：行可能（也可能不）由其列值唯一标识。 键列可能（也可能不）由 DBCOLUMNFLAGS_KEYCOLUMN 进行标记。|  
|DBPROP_UPDATABILITY|R/w： 读/写<br /><br /> 默认值： 0<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持所有 DBPROP_UPDATABILITY 值。 设置 DBPROP_UPDATABILITY 并不创建可修改的行集。 为了使行集变得可修改，请设置 DBPROP_IRowsetChange 或 DBPROP_IRowsetUpdate。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义提供程序特定的属性集 DBPROPSET_SQLSERVERROWSET，此表中所示。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COLUMN_ID|列：ColumnID<br /><br /> R/w： 只读<br /><br /> 类型： VT_U12 &#124; VT_ARRAY<br /><br /> 默认值：VT_EMPTY<br /><br /> 说明：表示当前 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 语句中的 COMPUTE 子句结果列的序号位置（从 1 开始）的整数值数组。 这是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口中等效的 ODBC sql_ca_ss_column_id 属性的属性。|  
|SSPROP_DEFERPREPARE|列：No<br /><br /> R/w： 读/写<br /><br /> 类型：VT_BOOL<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明： VARIANT_TRUE： 在准备好的执行，推迟命令准备，直到**icommand:: Execute**调用或执行元属性操作。 如果此属性设置为<br /><br /> VARIANT_FALSE： 准备语句时**icommandprepare:: Prepare**执行。|  
|SSPROP_IRowsetFastLoad|列：No<br /><br /> R/w： 读/写<br /><br /> 类型：VT_BOOL<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 将此属性设置为 variant_true，则可以打开通过一个快速加载行集**iopenrowset:: Openrowset**。 不能将此属性设置**icommandproperties:: Setproperties**。|  
|SSPROP_ISSAsynchStatus|列：No。<br /><br /> R/w： 读/写<br /><br /> 类型：VT_BOOL<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明： 将此属性设置为 variant_true，则可以使用的异步操作[ISSAsynchStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)接口。|  
|SSPROP_MAXBLOBLENGTH|列：No<br /><br /> R/w： 读/写<br /><br /> 类型：VT_I4<br /><br /> 默认值：访问接口不限制由服务器返回的文本大小，并且此属性值设置为其最大值。 例如，2147483647。<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口执行 SET TEXTSIZE 语句，以限制在 SELECT 语句中返回的二进制大型对象 (BLOB) 数据的长度。|  
|SSPROP_NOCOUNT_STATUS|列：NoCount<br /><br /> R/w： 只读<br /><br /> 类型：VT_BOOL<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：一个布尔值，表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 SET NOCOUNT ON/OFF 的状态。<br /><br /> VARIANT_TRUE：当 SET NOCOUNT 为 ON 时<br /><br /> VARIANT_FALSE：当 SET NOCOUNT 为 OFF 时|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|列：No<br /><br /> R/w： 读/写<br /><br /> 类型：VT_BSTR（允许 1-2000 个字符）<br /><br /> 默认值：空字符串<br /><br /> 说明：查询通知的消息文本。 这是用户定义的文本，没有确定的格式。|  
|SSPROP_QP_NOTIFICATION_OPTIONS|列：No<br /><br /> R/w： 读/写<br /><br /> 类型：VT_BSTR<br /><br /> 默认值：空字符串<br /><br /> 说明：查询通知选项。 在具有 `name=value` 的字符串中指定这些内容。 用户负责创建服务并从队列中读取通知。 查询通知选项字符串的语法为：<br /><br /> `service=<service-name>[;(local database=<database>&#124;broker instance=<broker instance>)]`<br /><br /> 例如：<br /><br /> `service=mySSBService;local database=mydb`|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|列：No<br /><br /> R/w： 读/写<br /><br /> 类型：VT_UI4<br /><br /> 默认值：432000 秒（5 天）<br /><br /> 最小值：1 秒<br /><br /> 最大值：2^31-1 秒<br /><br /> 说明：查询通知保持为活动状态的秒数。|  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  
