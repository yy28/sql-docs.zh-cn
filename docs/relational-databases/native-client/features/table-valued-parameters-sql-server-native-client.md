---
title: 表值参数 (SQL Server Native Client) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, table-valued parameters
- table-valued parameters (SQL Server Native Client)
ms.assetid: 5ee6bdcd-0309-4a20-b5c2-0e6b6839f34f
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 315bf2f69d53532952cad92fad3b92d89d5c697c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949802"
---
# <a name="table-valued-parameters-sql-server-native-client"></a>表值参数 (SQL Server Native Client)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  表值参数在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入，它们为将多个数据行传递到服务器提供了有效方式。 表值参数提供类似于参数数组的功能，但它们提供了更好的灵活性和与 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 的更紧密集成，并且可以极大地提高性能。 而参数数组不能在基于集的操作，还可以参与表值参数。  
  
 有关表值参数和 ODBC 的信息，请参阅[表值参数&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
 有关表值参数和 OLE DB 的信息，请参阅[表值参数&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
