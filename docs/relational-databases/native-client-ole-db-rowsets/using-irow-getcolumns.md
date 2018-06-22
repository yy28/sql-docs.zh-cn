---
title: 使用 IRow::GetColumns |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9924e5374909ec8ff9a6465b7e7d1b5c594faf25
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694585"
---
# <a name="using-irowgetcolumns"></a>使用 IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRow**实现允许到的列的只进顺序访问。 你可以访问具有一次对的行中的所有列**IRow::GetColumns**或调用**IRow::GetColumns**多次每次都访问行中的多个列。  
  
 多次调用**IRow::GetColumns**不应重叠。 例如，如果第一次调用到**IRow::GetColumns**检索到的列 1、 2 和 3，第二个调用**IRow::GetColumns**应该调用列 4、 5 和 6。 如果稍后调用**IRow::GetColumns**重叠，状态标志 （在 DBCOLUMNACCESS dwstatus 字段） 设置为 DBSTATUS_E_UNAVAILABLE。  
  
## <a name="see-also"></a>请参阅  
 [使用 IRow 提取单行](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
