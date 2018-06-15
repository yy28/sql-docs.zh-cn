---
title: IRowsetFastLoad (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d747a4892940effe8b5b21a7b9ceddbde1ff71aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948732"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRowsetFastLoad**接口公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]基于内存的大容量复制操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机客户端 OLE DB 提供程序使用者使用接口来快速将数据添加到现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 如果将会话的 SSPROP_ENABLEFASTLOAD 设置为 VARIANT_TRUE，则无法读取后续从该会话返回的行集中的数据。 当 SSPROP_ENABLEFASTLOAD 设置为 VARIANT_TRUE 时，在会话上创建的所有行集将是类型 IRowsetFastLoad。 IRowsetFastLoad 行集不支持行集提取功能;因此，无法读取从这些行集的数据。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|Description|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|标记一批插入的行的末尾并将这些行写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|将行添加到大容量复制行集中。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [大容量复制数据使用 IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [将 BLOB 数据发送到 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
