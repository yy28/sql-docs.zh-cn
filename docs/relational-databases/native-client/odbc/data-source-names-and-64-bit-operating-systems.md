---
title: 数据源名称和 64 位操作系统 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24af2f7d0d6feae7a7c4ab6c6e6635cb281f1ba0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43098743"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>数据源名称和 64 位操作系统
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  如果您要将某一应用程序构建为在 64 位操作系统上运行的 32 位应用程序并运行该应用程序，则必须使用 %windir%\SysWOW64\odbcad32.exe 中的 ODBC 管理器创建 ODBC 数据源。  
  
## <a name="remarks"></a>Remarks  
 64 位 Windows 操作系统具有以下两个 odbcad32.exe 文件：  
  
-   %SystemRoot%\system32\odbcad32.exe 用于为 64 位应用程序创建和维护数据源名称。  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe 用于为 32 位应用程序（包括在 64 位操作系统上运行的 32 位应用程序）创建和维护数据源名称。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
