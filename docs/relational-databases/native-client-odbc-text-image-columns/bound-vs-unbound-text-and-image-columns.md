---
title: 绑定与未绑定的 Text 和 Image 列 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e760707c97b9ac45d30b2d94163561324e60db5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790967"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>绑定与未绑定的 Text 和 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用服务器游标时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序经过优化，可不传输未绑定数据**文本**， **ntext**，或**映像**上的列时间**SQLFetch**执行。 **文本**， **ntext**，或**图像**数据不实际从服务器检索到应用程序问题[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)为列。  
  
 可以编写许多应用程序，以便无**文本**， **ntext**，或**图像**用户只需在游标中向上和向下滚动时显示数据。 当用户选择某一行以获取更多详细信息时，该应用程序然后可以调用**SQLGetData**检索**文本**， **ntext**，或者**映像**数据。 这可以避免传输**文本**， **ntext**，或**图像**数据对于任何行的用户不会不选择，因此可以避免传输非常大数据量。  
  
## <a name="see-also"></a>请参阅  
 [管理 Text 和 Image 列](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [游标行为](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
