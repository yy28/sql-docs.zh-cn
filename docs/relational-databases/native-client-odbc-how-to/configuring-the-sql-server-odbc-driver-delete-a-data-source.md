---
title: 删除数据源 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 70f7c6e02ef6f152f2a33462619e106d7b8569f1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102288"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>配置 SQL Server ODBC 驱动程序 - 删除数据源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  将 ODBC 应用程序用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本之前，必须了解如何升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本上的目录存储过程的版本，以及如何添加、删除和测试数据源。  
  
  可以通过以编程方式使用 ODBC 管理器删除数据源 (通过使用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md))，或通过删除文件 （如果文件数据源名称）。  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>通过使用 ODBC 管理器删除数据源  
  
1.  在**Control Panel**，打开**管理工具**，然后双击任一**ODBC 数据源 （64 位）** 或**ODBC 数据源 （32 位）**. 或者，也可以从命令提示符处运行 odbcad32.exe。  
  
2.  单击**用户 DSN**，**系统 DSN**，或**文件 DSN**选项卡。  
  
3.  选择要删除的数据源。  
  
4.  单击**删除**，然后确认删除。  
  
## <a name="example"></a>示例  
 若要以编程方式删除数据源，调用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)使用 ODBC_REMOVE_DSN 或 ODBC_REMOVE_SYS_DSN 作为第二个参数。  
  
 以下示例显示如何以编程方式删除数据源。  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include \<windows.h>  
#include \<odbcinst.h>  
  
int main() {   
   LPCSTR provider = "SQL Server";   // Windows SQL Server Driver  
   LPCSTR provider = "SQL Server";   // Windows SQL Server driver  
   LPCSTR provider2 = "SQL Server Native Client 11.0";   // SQL Server 2012 Native Client driver  
   LPCSTR dsnname = "DSN=data2";  
   BOOL retval = SQLConfigDataSource(NULL, ODBC_REMOVE_DSN, provider, dsnname);  
   std::cout << retval;   // 1 if successful  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [添加数据源&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
