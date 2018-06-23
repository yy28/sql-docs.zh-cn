---
title: 绑定 vs。未绑定文本和图像列 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5129c6b865723721bbb6f176893c950cdf905fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017723"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>绑定 vs。未绑定的文本和图像列
  使用服务器游标时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序进行了优化以不传输数据的未绑定**文本**， **ntext**，或**映像**上的列时间**SQLFetch**执行。 **文本**， **ntext**，或**映像**数据不实际从服务器检索之前应用程序问题[SQLGetData](../native-client-odbc-api/sqlgetdata.md)为列。  
  
 可以编写许多应用程序，以便不**文本**， **ntext**，或**映像**用户只需在光标中向上和向下滚动时，将显示数据。 应用程序时用户选择要获取更多详细信息行，然后可调用**SQLGetData**检索**文本**， **ntext**，或**映像**数据。 这将使传输**文本**， **ntext**，或**映像**数据的任何行用户不未选择，并因此可以防止非常大的传输大量数据。  
  
## <a name="see-also"></a>请参阅  
 [管理文本和图像列](managing-text-and-image-columns.md)   
 [游标行为](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  