---
title: "ADO 动态属性索引 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: f126cc040174725ded02bd320e54a76536c0d516
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="ado-dynamic-property-index"></a>ADO 动态 Property 索引
数据提供程序、 服务提供商和服务组件可以添加到的动态属性**属性**集合的未打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 打开这些对象时，给定的提供程序还可能会插入其他属性。 中列出了这些属性的一些[ADO 动态属性](../../../ado/reference/ado-api/ado-dynamic-properties.md)部分。 下列出中的特定提供程序的详细信息[附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)部分。  
  
 下表是每个标准的 OLE DB 提供程序动态属性的 ADO 和 OLE DB 名称 cross-indexes。 你的提供商可能此处添加属性多于列出的属性。 有关提供程序特定的动态属性的特定信息，请参阅提供程序文档。  
  
 OLE DB 程序员参考指 ADO 属性名称，术语"Description"。 有关这些标准属性的详细信息，搜索或浏览中的索引[OLE DB 文档](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)按其名称的 OLE DB 属性。  
  
## <a name="connection-dynamic-properties"></a>连接的动态属性  
  
|ADO 属性名称|OLE DB 属性名称|  
|-----------------------|--------------------------|  
|活动会话|DBPROP_ACTIVESESSIONS|  
|异步终止|DBPROP_ASYNCTXNABORT|  
|可异步提交|DBPROP_ASYNCTNXCOMMIT|  
|自动提交隔离级别|DBPROP_SESS_AUTOCOMMITISOLEVELS|  
|目录位置|DBPROP_CATALOGLOCATION|  
|目录术语|DBPROP_CATALOGTERM|  
|列定义|DBPROP_COLUMNDEFINITION|  
|连接超时值|DBPROP_INIT_TIMEOUT|  
|当前目录|DBPROP_CURRENTCATALOG|  
|数据源|DBPROP_INIT_DATASOURCE|  
|数据源名称|DBPROP_DATASOURCENAME|  
|线程处理模型的数据源对象|DBPROP_DSOTHREADMODEL|  
|DBMS 名称|DBPROP_DBMSNAME|  
|DBMS 版本|DBPROP_DBMSVER|  
|扩展的属性|DBPROP_INIT_PROVIDERSTRING|  
|按支持进行分组|DBPROP_GROUPBY|  
|异类表支持|DBPROP_HETEROGENEOUSTABLES|  
|标识符区分大小写|DBPROP_IDENTIFIERCASE|  
|初始目录|DBPROP_INIT_CATALOG|  
|隔离级别|DBPROP_SUPPORTEDTXNISOLEVELS|  
|隔离保留|DBPROP_SUPPORTEDTXNISORETAIN|  
|区域设置标识符|DBPROP_INIT_LCID|  
|位置|DBPROP_INIT_LOCATION|  
|最大索引大小|DBPROP_MAXINDEXSIZE|  
|最大行大小|DBPROP_MAXROWSIZE|  
|最大行大小包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|  
|在选择的最大表|DBPROP_MAXTABLESINSELECT|  
|模式|DBPROP_INIT_MODE|  
|多个参数集|DBPROP_MULTIPLEPARAMSETS|  
|多个结果|DBPROP_MULTIPLERESULTS|  
|多个存储对象|DBPROP_MULTIPLESTORAGEOBJECTS|  
|多表更新|DBPROP_MULTITABLEUPDATE|  
|NULL 的排序规则顺序|DBPROP_NULLCOLLATION|  
|NULL 串联行为|DBPROP_CONCATNULLBEHAVIOR|  
|OLE DB 服务|DBPROP_INIT_OLEDBSERVICES|  
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|  
|OLE 对象支持|DBPROP_OLEOBJECTS|  
|打开行集支持|DBPROP_OPENROWSETSUPPORT|  
|通过选择列表中的列进行排序|DBPROP_ORDERBYCOLUMNSINSELECT|  
|输出参数可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|  
|通过 Ref 访问器|DBPROP_BYREFACCESSORS|  
|密码|DBPROP_AUTH_PASSWORD|  
|持久性安全信息|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|  
|持久性 ID 类型|DBPROP_PERSISTENTIDTYPE|  
|准备中止行为|DBPROP_PREPAREABORTBEHAVIOR|  
|准备提交行为|DBPROP_PREPARECOMMITBEHAVIOR|  
|过程术语|DBPROP_PROCEDURETERM|  
|提示|DBPROP_INIT_PROMPT|  
|提供程序的友好名称|DBPROP_PROVIDERFRIENDLYNAME|  
|Provider Name|DBPROP_PROVIDERFILENAME|  
|提供程序版本|DBPROP_PROVIDERVER|  
|仅限读取的数据源|DBPROP_DATASOURCEREADONLY|  
|在命令行集转换|DBPROP_ROWSETCONVERSIONSONCOMMAND|  
|架构术语|DBPROP_SCHEMATERM|  
|架构使用情况|DBPROP_SCHEMAUSAGE|  
|SQL 支持|DBPROP_SQLSUPPORT|  
|结构化的存储|DBPROP_STRUCTUREDSTORAGE|  
|子查询支持|DBPROP_SUBQUERIES|  
|表术语|DBPROP_TABLETERM|  
|事务 DDL|DBPROP_SUPPORTEDTXNDDL|  
|用户 ID|DBPROP_AUTH_USERID|  
|用户名|DBPROP_USERNAME|  
|窗口句柄|DBPROP_INIT_HWND|  
  
## <a name="recordset-dynamic-properties"></a>记录集动态属性  
 请注意，**动态属性**的**记录集**对象超出范围 （变得不可用） 时转**记录集**已关闭。  
  
|ADO 属性名称|OLE DB 属性名称|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IrowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IrowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IrowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|访问顺序|DBPROP_ACCESSORDER|  
|仅限追加的行集|DBPROP_APPENDONLY|  
|异步行集处理|DBPROP_ROWSET_ASYNCH|  
|自动重新计算|DBPROP_ADC_AUTORECALC|  
|背景提取大小|DBPROP_ASYNCHFETCHSIZE|  
|后台线程优先级|DBPROP_ASYNCHTHREADPRIORITY|  
|批大小|DBPROP_ADC_BATCHSIZE|  
|阻止存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|书签类型|DBPROP_BOOKMARKTYPE|  
|Bookmarkable|DBPROP_IROWSETLOCATE|  
|排序的书签|DBPROP_ORDEREDBOOKMARKS|  
|缓存子行|DBPROP_ADC_CACHECHILDROWS|  
|缓存延迟的列|DBPROP_CACHEDEFERRED|  
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|  
|列权限|DBPROP_COLUMNRESTRICT|  
|列集通知|DBPROP_NOTIFYCOLUMNSET|  
|可写的列|DBPROP_MAYWRITECOLUMN|  
|命令超时|DBPROP_COMMANDTIMEOUT|  
|光标引擎版本|DBPROP_ADC_CEVER|  
|延迟列|DBPROP_DEFERRED|  
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|  
|向后获取|DBPROP_CANFETCHBACKWARDS|  
|筛选器操作|DBPROP_FILTERCOMPAREOPS|  
|查找操作|DBPROP_FINDCOMPAREOPS|  
|隐藏的列 （计数）|DBPROP_HIDDENCOLUMNS|  
|保存行|DBPROP_CANHOLDROWS|  
|固定的行|DBPROP_IMMOBILEROWS|  
|初始提取大小|DBPROP_ASYNCHPREFETCHSIZE|  
|文本书签|DBPROP_LITERALBOOKMARKS|  
|文本行标识|DBPROP_LITERALIDENTITY|  
|维护更改状态|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|打开的最大行数|DBPROP_MAXOPENROWS|  
|最大挂起行|DBPROP_MAXPENDINGROWS|  
|最大行数|DBPROP_MAXROWS|  
|内存使用量|DBPROP_MEMORYUSAGE|  
|通知粒度|DBPROP_NOTIFICATIONGRANULARITY|  
|通知阶段|DBPROP_NOTIFICATIONPHASES|  
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|  
|可见的其他用户的更改|DBPROP_OTHERUPDATEDELETE|  
|其他可见插入|DBPROP_OTHERINSERT|  
|拥有更改可见|DBPROP_OWNUPDATEDELETE|  
|自己插入可见|DBPROP_OWNINSERT|  
|中止时保留|DBPROP_ABORTPRESERVE|  
|提交时保留|DBPROP_COMMITPRESERVE|  
|Private1||  
|快速重新启动|DBPROP_QUICKRESTART|  
|可重入事件|DBPROP_REENTRANTEVENTS|  
|删除已删除的行|DBPROP_REMOVEDELETED|  
|报告多个更改|DBPROP_REPORTMULTIPLECHANGES|  
|重新调整形状名称|DBPROP_ADC_RESHAPENAME|  
|重新同步命令|DBPROP_ADC_CUSTOMRESYNCH|  
|返回挂起的插入|DBPROP_RETURNPENDINGINSERTS|  
|行删除通知|DBPROP_NOTIFYROWDELETE|  
|行的第一个更改通知|DBPROP_NOTIFYROWFIRSTCHANGE|  
|行插入通知|DBPROP_NOTIFYROWINSERT|  
|行的权限|DBPROP_ROWRESTRICT|  
|行重新同步通知|DBPROP_NOTIFYROWRESYNCH|  
|线程处理模型的行|DBPROP_ROWTHREADMODEL|  
|行撤消更改通知|DBPROP_NOTIFYROWUNDOCHANGE|  
|行撤消删除通知|DBPROP_NOTIFYROWUNDODELETE|  
|行撤消插入通知|DBPROP_NOTIFYROWUNDOINSERT|  
|行更新通知|DBPROP_NOTIFYROWUPDATE|  
|行集提取位置更改通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|  
|行集版本通知|DBPROP_NOTIFYROWSETRELEASE|  
|向后滚动|DBPROP_CANSCROLLBACKWARDS|  
|服务器游标|DBPROP_SERVERCURSOR|  
|跳过删除书签|DBPROP_BOOKMARKSKIPPED|  
|强行标识|DBPROP_STRONGIDENTITY|  
|唯一的目录|DBPROP_ADC_UNIQUECATALOG|  
|唯一行|DBPROP_UNIQUEROWS|  
|唯一的架构|DBPROP_ADC_UNIQUESCHEMA|  
|唯一表|DBPROP_ADC_UNIQUETABLE|  
|可更新性|DBPROP_UPDATABILITY|  
|更新条件|DBPROP_ADC_UPDATECRITERIA|  
|更新重新同步|DBPROP_ADC_UPDATERESYNC|  
|使用书签|DBPROP_BOOKMARKS|