---
title: 书签 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序中的书签
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- OLE DB Driver for SQL Server, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 49131352cc8c351c1115c9fe3570d4431c0ba545
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781336"
---
# <a name="bookmarks"></a>书签
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  书签支持使用者快速返回到某行。 利用书签，使用者可以根据书签值对行进行随机访问。 行集中的列 0 为书签列。 使用者可将绑定结构的 dwFlag 字段值设置为 DBCOLUMNSINFO_ISBOOKMARK，以指示将该列用作书签。 使用者还可将行集属性 DBPROP_BOOKMARKS 设置为 VARIANT_TRUE。 这样可使行集中包含列 0。 然后，可使用 IRowsetLocate::GetRowsAt 方法提取行（起始行的位置为书签加上一个偏移量得到的位置）  。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
