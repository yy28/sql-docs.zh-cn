---
title: 执行时数据和 Text、ntext 或 Image 列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 404fade34862fe4705ec440eef7f466a9073250b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039298"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>执行时数据和 Text、ntext 或 Image 列
  使用 ODBC 执行时数据功能，应用程序能够对绑定列或参数使用非常大的数据量。 检索非常大的**text**、 **ntext**或**image**列时，应用程序可能无法简单地分配大型缓冲区，将列绑定到缓冲区，并提取行。 更新非常大的**text**、 **ntext**或**image**列时，应用程序可能无法简单地分配大型缓冲区，将其绑定到 SQL 语句中的参数标记，然后执行该语句。 在这些情况下，应用程序必须将[SQLGetData](../native-client-odbc-api/sqlgetdata.md)或[SQLPutData](../native-client-odbc-api/sqlputdata.md)与它的执行时数据选项一起使用。  
  
## <a name="see-also"></a>另请参阅  
 [管理 Text 和 Image 列](managing-text-and-image-columns.md)  
  
  
