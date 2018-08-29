---
title: SQL Server Native Client 的组件 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3829f6693968cc988cb7bb4df7a444f61e7ef342
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43101355"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client 的组件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 包含下列组件：  
  
|组件|Description|  
|---------------|-----------------|  
|sqlncli11.dll|包含所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 功能的动态链接库 (DLL) 文件。 它包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序。|  
|sqlnclir11.rll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 库附带的资源文件。|   
|sqlncli.h|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 头文件，其中包含使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时所需的所有新定义。 该头文件取代了 odbcss.h 和 sqloledb.h 头文件。<br /><br /> 注意： 不能引用 sqlncli.h 和 odbcss.h 在同一程序中，但可以引用 sqlncli.h 和 sqloledb.h 同一程序中的，只要先定义了 sqloledb.h。|  
|sqlncli11.lib|库文件需要直接调用**bcp**一部分的实用工具函数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。<br /><br /> 注意： 如果你确实在编程代码中引用 sqlncli11.lib 文件，您需要确保 sqlncli11.dll 文件位于系统路径中，在和中的用户的系统路径的应用程序使用。|  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Native Client 生成应用程序](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
