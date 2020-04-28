---
title: 数据源示例 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306518"
---
# <a name="data-source-example"></a>数据源示例
在运行 Microsoft® Windows NT® Server/Windows 2000 Server、Microsoft Windows NT Workstation/Windows 2000 Professional 或 Microsoft Windows®95/98 的计算机上，计算机数据源信息存储在注册表中。 根据信息存储在哪个注册表项，数据源被称为 "*用户数据*源" 或 "*系统数据源*"。 用户数据源存储在 HKEY_CURRENT_USER 项下，仅对当前用户可用。 系统数据源存储在 HKEY_LOCAL_MACHINE 密钥下，并可由一台计算机上的多个用户使用。 它们还可以由系统范围服务使用，即使没有用户登录到计算机，也可以访问数据源。 有关用户和系统数据源的详细信息，请参阅[SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假设用户有三个用户数据源：使用 Oracle DBMS 的人员和库存;和工资单，使用 Microsoft SQL Server DBMS。 数据源的注册表值可能是：  
  
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
