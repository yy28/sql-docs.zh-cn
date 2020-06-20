---
title: 添加数据源（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: rothja
ms.author: jroth
ms.openlocfilehash: c1919d516c8ad12b9e89eb4759186d8ddde752d5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018947"
---
# <a name="add-a-data-source-odbc"></a>添加数据源 (ODBC)
  您可以使用 ODBC 管理器（通过使用[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)）或创建文件来添加数据源。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理器添加数据源  
  
1.  从 "**控制面板**" 中，访问 "**管理工具**"，然后访问 "**数据源（ODBC）**"。 或者，可以调用 odbcad32.exe。  
  
2.  单击 "**用户 dsn**"、"**系统 dsn**" 或 "**文件 dsn** " 选项卡，然后单击 "**添加**"。  
  
3.  单击 " **SQL Server**"，然后单击 "**完成**"。  
  
4.  完成创建到 SQL Server 的新数据源向导中的步骤。  
  
### <a name="to-add-a-data-source-programmatically"></a>以编程方式添加数据源  
  
1.  调用[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) ，并将第二个参数设置为 ODBC_ADD_DSN 或 ODBC_ADD_SYS_DSN。  
  
### <a name="to-add-a-file-data-source"></a>添加文件数据源  
  
1.  使用连接字符串中的 SAVEFILE = file_name 参数调用[SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) 。 如果连接成功，则 ODBC 驱动程序将使用 SAVEFILE 参数指向的位置中的连接参数创建一个文件数据源。  
  
## <a name="see-also"></a>另请参阅  
 [配置 SQL Server ODBC 驱动程序操作指南主题](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  
