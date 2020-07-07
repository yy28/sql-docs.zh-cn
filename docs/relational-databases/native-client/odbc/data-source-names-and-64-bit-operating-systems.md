---
title: 数据源名称和64位操作系统 |Microsoft Docs
description: 了解如何使用 ODBC 管理器通过创建 ODBC 数据源，在64位操作系统上构建并运行应用程序作为32位应用程序。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f71694caf5b9e4a27ca07abc469064dab1dd5ff4
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009762"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>数据源名称和 64 位操作系统
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  如果您要将某一应用程序构建为在 64 位操作系统上运行的 32 位应用程序并运行该应用程序，则必须使用 %windir%\SysWOW64\odbcad32.exe 中的 ODBC 管理器创建 ODBC 数据源。  
  
## <a name="remarks"></a>注解  
 64 位 Windows 操作系统具有以下两个 odbcad32.exe 文件：  
  
-   %SystemRoot%\system32\odbcad32.exe 用于为 64 位应用程序创建和维护数据源名称。  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe 用于为 32 位应用程序（包括在 64 位操作系统上运行的 32 位应用程序）创建和维护数据源名称。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
