---
title: 'Irowsetfastload:: Commit (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 745282c1d1e8fa36c9d0a407ac32171304d05197
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417166"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  标记一批插入的行的末尾并将这些行写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 有关示例，请参阅[大容量复制数据使用 IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md)并[将 BLOB 数据发送到 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Commit(  
BOOL   
fDone  
);  
  
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
 在以前失效的大容量复制行集上调用该方法**irowsetfastload:: Commit**方法。  
  
## <a name="remarks"></a>Remarks  
 一个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口大容量复制行集的行为与延迟更新模式的行集相同。 用户插入通过行集的行数据，如插入的行的处理方式相同行集支持上挂起插入**IRowsetUpdate**。  
  
 使用者必须调用**提交**大容量复制行集要写入到插入的行上的方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表中一样**irowsetupdate:: Update**方法用于将挂起到行提交SQL Server 的实例。  
  
 如果使用者释放对大容量复制行集而无需调用其引用**提交**方法，所有插入都将丢失以前未写入的行数。  
  
 使用者可以通过调用执行批处理插入的行**提交**方法替换*fDone*参数设置为 FALSE。 当*fDone*是设置为 TRUE，行集变为无效。 无效的大容量复制行集仅支持**ISupportErrorInfo**接口并**irowsetfastload:: Release**方法。  
  
## <a name="see-also"></a>请参阅  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
