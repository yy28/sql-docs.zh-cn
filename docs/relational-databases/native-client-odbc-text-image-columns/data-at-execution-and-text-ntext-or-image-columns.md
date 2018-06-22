---
title: 执行中的数据和 Text、 ntext 或 Image 列 |Microsoft 文档
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
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56cf9e564eb21d0036b61be0fde1404ed1dee486
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694628"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>执行时数据和 Text、ntext 或 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用 ODBC 执行时数据功能，应用程序能够对绑定列或参数使用非常大的数据量。 检索非常大时**文本**， **ntext**，或**映像**列，应用程序不可以为能够只需分配极大的缓冲区，将列绑定到的缓冲区，并提取行。 更新非常大时**文本**， **ntext**，或**映像**列，应用程序可能不能只需分配极大的缓冲区，将其绑定到 SQL 中的参数标记语句，然后执行该语句。 在这些情况下，应用程序必须使用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)包括其执行中的数据选项。  
  
## <a name="see-also"></a>请参阅  
 [管理 Text 和 Image 列](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
