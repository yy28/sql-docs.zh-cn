---
title: IRowsetFastLoad::Commit (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56afd40607a212c9def34ebdef302ac685da51ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32943900"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  标记一批插入的行的末尾并将这些行写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 有关示例，请参阅[大容量复制数据使用 IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)和[将 BLOB 数据发送到 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>参数  
 *fDone*[in]  
 如果是 FALSE，则行集保持有效性，并且可由使用者用于插入其他行。 如果是 TRUE，则行集失去有效性，并且使用者无法执行进一步的插入。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功，并且所有插入的数据已写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。  
  
 E_FAIL  
 发生了特定于访问接口的错误。 从访问接口检索特定错误文本的错误信息。  
  
 E_UNEXPECTED  
 该方法调用以前失效的大容量复制行集上**IRowsetFastLoad::Commit**方法。  
  
## <a name="remarks"></a>注释  
 A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序大容量复制行集为延迟更新模式行集的行为。 插入的行在用户插入通过行集的行数据，如将被视为以相同的方式为挂起行集支持插入**IRowsetUpdate**。  
  
 使用者必须调用**提交**大容量复制行集写入到插入的行上的方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]方式与相同的表**IRowsetUpdate::Update**方法用于提交挂起的行SQL Server 的实例。  
  
 如果使用者释放其引用而不调用大容量复制行集上的**提交**方法中，所有插入以前未写入的行都将丢失。  
  
 使用者可以通过调用执行批处理插入的行**提交**方法替换*fDone*参数设置为 FALSE。 当*fDone*是设置为 TRUE，行集将变为无效。 无效的大容量复制行集仅支持**ISupportErrorInfo**接口和**IRowsetFastLoad::Release**方法。  
  
## <a name="see-also"></a>另请参阅  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
