---
title: 执行时数据和 Text、 ntext 或 Image 列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e19381ce928e3eca5e80b02b92c61dc666d19ebe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703925"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>执行时数据和 Text、ntext 或 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用 ODBC 执行时数据功能，应用程序能够对绑定列或参数使用非常大的数据量。 当检索很大**文本**， **ntext**，或**图像**列，应用程序可能无法简单地分配大型缓冲区，将列绑定到缓冲区，并提取行。 当更新很大**文本**， **ntext**，或**图像**列，该应用程序可能不能简单地分配大型缓冲区，将其绑定到 SQL 中的参数标记语句，然后执行该语句。 在这些情况下，应用程序必须使用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)包括其执行时数据选项。  
  
## <a name="see-also"></a>请参阅  
 [管理 Text 和 Image 列](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
