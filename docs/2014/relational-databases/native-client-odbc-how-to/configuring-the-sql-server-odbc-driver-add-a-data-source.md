---
title: 添加数据源 (ODBC) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 822ac0f5d2e228a982368849ed1c409ef63765ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126069"
---
# <a name="add-a-data-source-odbc"></a>添加数据源 (ODBC)
  你可以以编程方式使用 ODBC 管理器中，添加数据源 (通过使用[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md))，或通过创建的文件。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理器添加数据源  
  
1.  从**控制面板**，访问**管理工具**然后**数据源 (ODBC)**。 或者，可以调用 odbcad32.exe。  
  
2.  单击**用户 DSN**，**系统 DSN**，或**文件 DSN**选项卡上，并依次**添加**。  
  
3.  单击**SQL Server**，然后单击**完成**。  
  
4.  完成创建到 SQL Server 的新数据源向导中的步骤。  
  
### <a name="to-add-a-data-source-programmatically"></a>以编程方式添加数据源  
  
1.  调用[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)与设置为 ODBC_ADD_DSN 或 ODBC_ADD_SYS_DSN 第二个参数。  
  
### <a name="to-add-a-file-data-source"></a>添加文件数据源  
  
1.  调用[SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) SAVEFILE 为连接字符串中的文件名参数。 如果连接成功，则 ODBC 驱动程序将使用 SAVEFILE 参数指向的位置中的连接参数创建一个文件数据源。  
  
## <a name="see-also"></a>请参阅  
 [配置 SQL Server ODBC 驱动程序操作说明主题](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  