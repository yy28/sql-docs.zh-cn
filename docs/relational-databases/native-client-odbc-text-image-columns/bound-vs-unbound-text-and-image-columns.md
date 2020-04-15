---
title: 绑定与未绑定文本和图像列 |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cfa05f7019342d63ab6f3092c3b6df5ae6e8daa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297728"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>绑定与未绑定的 Text 和 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  使用服务器游标时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序经过优化，以在执行**SQLFetch**时不传输未绑定**文本****、ntext**或**图像**列的数据。 在应用程序为列发出[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)之前，实际上不会从服务器检索**文本****、ntext**或**图像**数据。  
  
 可以编写许多应用程序，以便在用户只是在光标中上下滚动时不显示**文本****、ntext**或**图像**数据。 当用户选择一行以获取更多详细信息时，应用程序可以调用**SQLGetData**来检索**文本****、ntext**或**图像**数据。 这将防止为用户未选择的任何行传输**文本****、ntext**或**图像**数据，因此可以防止传输大量数据。  
  
## <a name="see-also"></a>另请参阅  
 [管理文本和图像列](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [游标行为](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
