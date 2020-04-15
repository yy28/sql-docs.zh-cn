---
title: 数据源示例 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306518"
---
# <a name="data-source-example"></a>数据源示例
在运行 Microsoft ® Windows NT® 服务器/Windows 2000 服务器、微软 Windows NT 工作站/Windows 2000 专业版或 Microsoft Windows ® 95/98 的计算机中，计算机数据源信息存储在注册表中。 根据信息存储的注册表项，数据源称为*用户数据源*或*系统数据源*。 用户数据源存储在HKEY_CURRENT_USER键下，并且仅对当前用户可用。 系统数据源存储在HKEY_LOCAL_MACHINE键下，可以在一台计算机上由多个用户使用。 它们也可以由系统范围的服务使用，即使没有用户登录到计算机，这些服务也可以访问数据源。 有关用户和系统数据源的详细信息，请参阅[SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假设用户有三个用户数据源：使用 Oracle DBMS 的人员和清单;和工资单，它使用微软 SQL Server DBMS。 数据源的注册表值可能是：  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 工资单数据源的注册表值可能是：  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
