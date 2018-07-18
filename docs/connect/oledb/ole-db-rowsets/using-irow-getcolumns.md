---
title: 使用 IRow::GetColumns |Microsoft 文档
description: 使用 IRow::GetColumns 访问行中的所有列
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: be29bec8c92036b6d53a56f4aab8ccdfc8e8c369
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690050"
---
# <a name="using-irowgetcolumns"></a>使用 IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IRow**实现允许到的列的只进顺序访问。 你可以访问具有一次对的行中的所有列**IRow::GetColumns**或调用**IRow::GetColumns**多次每次都访问行中的多个列。  
  
 多次调用**IRow::GetColumns**不应重叠。 例如，如果第一次调用到**IRow::GetColumns**检索到的列 1、 2 和 3，第二个调用**IRow::GetColumns**应该调用列 4、 5 和 6。 如果稍后调用**IRow::GetColumns**重叠，状态标志 （在 DBCOLUMNACCESS dwstatus 字段） 设置为 DBSTATUS_E_UNAVAILABLE。  
  
## <a name="see-also"></a>请参阅  
 [使用 IRow 提取单行](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
