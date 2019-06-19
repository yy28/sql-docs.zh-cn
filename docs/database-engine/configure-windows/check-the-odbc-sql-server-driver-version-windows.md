---
title: 检查 ODBC SQL Server 驱动程序版本 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- driver version number [ODBC]
- ODBC drivers, version number
ms.assetid: 43451080-a562-4231-b1d4-1ba35ca0ea79
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fb6646d96991785b7c94a48ad4601fdcc6e35b60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799548"
---
# <a name="check-the-odbc-sql-server-driver-version-windows"></a>检查 ODBC SQL Server 驱动程序版本 (Windows)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  您的计算机可能包含来自 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 和其他公司的多种 ODBC 驱动程序。 本主题介绍如何使用 Windows **“ODBC 数据源管理器”** 来查看已安装的 ODBC 驱动程序的版本。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-check-the-odbc-sql-server-driver-version-32-bit-odbc"></a>检查 ODBC SQL Server 驱动程序版本（32 位 ODBC）  
  
-   在 **“ODBC 数据源管理器”** 中，单击 **“驱动程序”** 选项卡。  
  
     有关 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 项的信息显示在 **“版本”** 列中。  


> [!NOTE]  
>  对于与 SQL 数据库的 Azure Active Directory 身份验证的连接，请安装最新的驱动程序，如 [ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)。   

  
## <a name="see-also"></a>另请参阅  
 [打开 ODBC 数据源管理器](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
  
