---
title: 绑定 vs。未绑定文本和图像列 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 04d0fa5a7973d0a0477461b7e485e6022c51922a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>绑定 vs。未绑定的文本和图像列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用服务器游标时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序进行了优化以不传输数据的未绑定**文本**， **ntext**，或**映像**列时**SQLFetch**执行。 **文本**， **ntext**，或**映像**数据不实际从服务器检索之前应用程序问题[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)的列。  
  
 可以编写许多应用程序，以便不**文本**， **ntext**，或**映像**用户只需在光标中向上和向下滚动时，将显示数据。 应用程序时用户选择要获取更多详细信息行，然后可调用**SQLGetData**检索**文本**， **ntext**，或**映像**数据。 这将使传输**文本**， **ntext**，或**映像**数据的任何行用户不未选择，并因此可以防止传输的数据量非常大。  
  
## <a name="see-also"></a>另请参阅  
 [管理文本和图像列](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [游标行为](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
