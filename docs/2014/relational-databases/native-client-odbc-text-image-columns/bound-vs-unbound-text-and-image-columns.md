---
title: 绑定与未绑定的 Text 和 Image 列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 1bf8ac0cf868394d9aa8063220939feee69ac2f6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108257"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>绑定与未绑定的 Text 和 Image 列
  使用服务器游标时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序经过优化，可不传输未绑定数据**文本**， **ntext**，或**映像**上的列时间**SQLFetch**执行。 **文本**， **ntext**，或**图像**数据不实际从服务器检索到应用程序问题[SQLGetData](../native-client-odbc-api/sqlgetdata.md)为列。  
  
 可以编写许多应用程序，以便无**文本**， **ntext**，或**图像**用户只需在游标中向上和向下滚动时显示数据。 当用户选择某一行以获取更多详细信息时，该应用程序然后可以调用**SQLGetData**检索**文本**， **ntext**，或者**映像**数据。 这可以避免传输**文本**， **ntext**，或**图像**数据对于任何行的用户不会不选择，因此可以避免传输非常大数据量。  
  
## <a name="see-also"></a>请参阅  
 [管理 Text 和 Image 列](managing-text-and-image-columns.md)   
 [游标行为](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
