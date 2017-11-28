---
title: "添加数据源 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 69b2056a8d9b51f6e75eb68a3323665fcc956a92
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>配置 SQL Server ODBC 驱动程序-添加数据源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  将 ODBC 应用程序用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本之前，必须了解如何升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本上的目录存储过程的版本，以及如何添加、删除和测试数据源。  
  
  你可以以编程方式使用 ODBC 管理器中，添加数据源 (通过使用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md))，或通过创建的文件。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理器添加数据源  
  
1.  从**控制面板**，访问**管理工具**然后**ODBC 数据源 （64 位）**或**ODBC 数据源 （32 位）**. 或者，可以调用 odbcad32.exe。  
  
2.  单击**用户 DSN**，**系统 DSN**，或**文件 DSN**选项卡上，并依次**添加**。  
  
3.  单击**SQL Server**，然后单击**完成**。  
  
4.  完成中的步骤**创建新的数据源到 SQL Server**向导。  
  
### <a name="to-add-a-data-source-programmatically"></a>以编程方式添加数据源  
  
1.  调用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)与设置为 ODBC_ADD_DSN 或 ODBC_ADD_SYS_DSN 第二个参数。  
  
### <a name="to-add-a-file-data-source"></a>添加文件数据源  
  
1.  调用[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) SAVEFILE 为连接字符串中的文件名参数。 如果连接成功，则 ODBC 驱动程序将使用 SAVEFILE 参数指向的位置中的连接参数创建一个文件数据源。  
  
## <a name="see-also"></a>另请参阅  
[删除数据源 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
