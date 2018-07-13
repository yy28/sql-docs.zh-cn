---
title: 执行时数据和 Text、 ntext 或 Image 列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0e03c12fe94755e42c5838a66c85242cae59a62
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416246"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>执行时数据和 Text、ntext 或 Image 列
  使用 ODBC 执行时数据功能，应用程序能够对绑定列或参数使用非常大的数据量。 当检索很大**文本**， **ntext**，或**图像**列，应用程序可能无法简单地分配大型缓冲区，将列绑定到缓冲区，并提取行。 当更新很大**文本**， **ntext**，或**图像**列，该应用程序可能不能简单地分配大型缓冲区，将其绑定到 SQL 中的参数标记语句，然后执行该语句。 在这些情况下，应用程序必须使用[SQLGetData](../native-client-odbc-api/sqlgetdata.md)或[SQLPutData](../native-client-odbc-api/sqlputdata.md)包括其执行时数据选项。  
  
## <a name="see-also"></a>请参阅  
 [管理 Text 和 Image 列](managing-text-and-image-columns.md)  
  
  
