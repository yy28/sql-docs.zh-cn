---
title: "数据源示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85eae404d4fa0ab739c699c8f120c76122c8ba67
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-example"></a>数据源示例
运行 Microsoft® Windows NT® Server/Windows 2000 Server、 Microsoft Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows® 95/98，机数据的计算机上源信息存储在注册表中。 具体取决于哪一个注册表密钥信息存储在下，数据源称为*用户数据源*或*系统数据源*。 用户数据源存储在 HKEY_CURRENT_USER 键下，并且仅适用于当前用户。 系统数据源存储在 HKEY_LOCAL_MACHINE 键下，并且可以由一台计算机上的多个用户。 它们还可以使用由系统级服务，即使没有用户登录到计算机，然后可以获得对数据源的访问。 有关用户和系统数据源的详细信息，请参阅[SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假设用户具有三个用户数据源： 人员和清单，使用 Oracle DBMS 中;和使用 Microsoft SQL Server DBMS 的工资支付。 数据源的注册表值可能是：  
  
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
  
 并且可能工资单数据源的注册表值：  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
