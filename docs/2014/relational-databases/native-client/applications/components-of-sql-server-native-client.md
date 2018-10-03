---
title: SQL Server Native Client 的组件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 329ffa78471ead02b1431a41d898cfc43ca65684
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141037"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client 的组件
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 包含下列组件：  
  
|组件|Description|  
|---------------|-----------------|  
|sqlncli11.dll|包含所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 功能的动态链接库 (DLL) 文件。 它包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序。|  
|sqlnclir11.rll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 库附带的资源文件。|  
|s10ch_sqlncli.chm|数据源向导帮助文件，对如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口创建 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据源作了文字说明。|  
|sqlncli.h|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 头文件，其中包含使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时所需的所有新定义。 该头文件取代了 odbcss.h 和 sqloledb.h 头文件。 **注意：** 不能引用 sqlncli.h 和 odbcss.h 在同一程序中，但可以引用 sqlncli.h 和 sqloledb.h 同一程序中的，只要先定义了 sqloledb.h。|  
|sqlncli11.lib|库文件需要直接调用**bcp**一部分的实用工具函数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。 **注意：** 如果你确实在编程代码中引用 sqlncli11.lib 文件，则需要确保 sqlncli11.dll 文件位于系统路径中，在和中的用户的系统路径的应用程序使用。|  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Native Client 生成应用程序](building-applications-with-sql-server-native-client.md)  
  
  
