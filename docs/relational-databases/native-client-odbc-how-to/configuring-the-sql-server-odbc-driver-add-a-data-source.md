---
title: 添加数据源 （ODBC） |微软文档
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55ae4f357aa850f6b3ff4ba9cca0b59a2ccbc570
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298311"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>配置 SQL Server ODBC 驱动程序 - 添加数据源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  将 ODBC 应用程序用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本之前，必须了解如何升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本上的目录存储过程的版本，以及如何添加、删除和测试数据源。  
  
  您可以通过使用 ODBC 管理员以编程方式（使用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)）或创建文件来添加数据源。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理器添加数据源  
  
1.  从**控制面板**，访问**管理工具**，然后访问**ODBC 数据源 （64 位）** 或**ODBC 数据源 （32 位）。** 或者，可以调用 odbcad32.exe。  
  
2.  单击**用户 DSN、****系统 DSN**或**文件 DSN**选项卡，然后单击"**添加**"。  
  
3.  单击**SQL 服务器**，然后单击 **"完成**"。  
  
4.  完成 **"向 SQL 服务器创建新数据源**"中的步骤。  
  
### <a name="to-add-a-data-source-programmatically"></a>以编程方式添加数据源  
  
1.  使用第二个参数设置为ODBC_ADD_DSN或ODBC_ADD_SYS_DSN调用[SQLConfigDataSource。](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)  
  
### <a name="to-add-a-file-data-source"></a>添加文件数据源  
  
1.  使用连接字符串中的 SAVEFILE_file_name 参数调用[SQLDriverConnect。](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 如果连接成功，则 ODBC 驱动程序将使用 SAVEFILE 参数指向的位置中的连接参数创建一个文件数据源。  
  
## <a name="see-also"></a>另请参阅  
[删除数据源&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
