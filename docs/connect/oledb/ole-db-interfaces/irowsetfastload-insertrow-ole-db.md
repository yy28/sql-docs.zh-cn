---
title: IRowsetFastLoad::InsertRow (OLE DB) |Microsoft 文档
description: IRowsetFastLoad::InsertRow (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 59fde3a16ea1e79587150307da12d917fd7e9a82
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689190"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  将行添加到大容量复制行集中。 有关示例，请参阅[大容量复制数据使用 IRowsetFastLoad &#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)和[将 BLOB 数据发送到 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>参数  
 *hAccessor*[in]  
 定义大容量复制的行数据的取值函数句柄。 引用的取值函数为行取值函数，将绑定包含数据值的使用者拥有的内存。  
  
 *pData*[in]  
 指向包含数据值的使用者所拥有内存的指针。 有关详细信息，请参阅[DBBINDING 结构](http://go.microsoft.com/fwlink/?LinkId=65955)。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。 所有列的任何绑定状态值都具有值 DBSTATUS_S_OK 或 DBSTATUS_S_NULL。  
  
 E_FAIL  
 出现了错误。 从行集的错误接口中发出错误信息。  
  
 E_INVALIDARG  
 *PData*参数已设置为 NULL 指针。  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL 无法分配足够内存来完成该请求。  
  
 E_UNEXPECTED  
 该方法调用以前失效的大容量复制行集上[IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)方法。  
  
 DB_E_BADACCESSORHANDLE  
 *HAccessor*使用者提供的自变量无效。  
  
 DB_E_BADACCESSORTYPE  
 指定的取值函数不是行取值函数，或者未指定使用者拥有的内存。  
  
## <a name="remarks"></a>Remarks  
 使用者将数据转换成错误[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]列的数据类型会导致从 OLE DB 驱动程序 E_FAIL 返回 SQL Server。 可以将数据传输到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上任何**InsertRow**方法或仅在**提交**方法。 使用者应用程序可以调用**InsertRow**多次具有错误的数据之前收到数据类型转换错误存在的通知方法。 因为**提交**方法可确保，所有数据进行正确都指定使用者，使用者可以使用**提交**方法相应地根据需要的数据进行验证。  
  
 用于 SQL Server 成批复制行集的 OLE DB 驱动程序是只写。 SQL Server 的 OLE DB 驱动程序公开允许使用者查询的行集的任何方法。 若要终止处理，使用者可以释放其引用上[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)接口而不调用**提交**方法。 没有用于进行以下操作的设备：访问行集中使用者插入的行、更改其值或从行集中逐一删除该行。  
  
 大容量复制行在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的服务器上进行了格式化。 可能已针对连接或会话（例如 ANSI_PADDING）设置的任何选项均会影响行格式。 默认情况下，可通过 OLE DB 驱动程序执行 SQL Server 的任何连接的情况下，此选项设置上。  
  
## <a name="see-also"></a>请参阅  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
