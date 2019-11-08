---
title: 书签 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- SQL Server Native Client OLE DB provider, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
ms.assetid: 7d9076f2-bf9c-452e-b816-70371a0c1644
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8de737a09c09a04b850e79bb1368d421465cb230
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789054"
---
# <a name="bookmarks"></a>书签
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  书签支持使用者快速返回到某行。 利用书签，使用者可以根据书签值对行进行随机访问。 行集中的列 0 为书签列。 使用者可将绑定结构的 dwFlag 字段值设置为 DBCOLUMNSINFO_ISBOOKMARK，以指示将该列用作书签。 使用者还可将行集属性 DBPROP_BOOKMARKS 设置为 VARIANT_TRUE。 这样可使行集中包含列 0。 然后，可使用 IRowsetLocate::GetRowsAt 方法提取行（起始行的位置为书签加上一个偏移量得到的位置）。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
