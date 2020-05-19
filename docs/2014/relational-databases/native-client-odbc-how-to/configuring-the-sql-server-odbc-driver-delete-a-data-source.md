---
title: 删除数据源（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c87d0123c5174461e4e3470b4e77ccb4bc5b10a1
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701895"
---
# <a name="delete-a-data-source-odbc"></a>删除数据源 (ODBC)
  您可以使用 ODBC 管理器、以编程方式（通过使用[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)）或通过删除文件（如果是文件数据源名称）来删除数据源。  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>通过使用 ODBC 管理器删除数据源  
  
1.  在 "**控制面板**" 中，打开 "**管理工具**"，然后双击 "**数据源（ODBC）**"。 或者，也可以从命令提示符处运行 odbcad32.exe。  
  
2.  单击 "**用户 dsn**"、"**系统 dsn**" 或 "**文件 dsn** " 选项卡。  
  
3.  单击要删除的数据源。  
  
4.  单击 "**删除**"，然后确认删除。  
  
## <a name="example"></a>示例  
 若要以编程方式删除数据源，请使用 ODBC_REMOVE_DSN 或 ODBC_REMOVE_SYS_DSN 作为第二个参数来调用[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) 。  
  
 以下示例显示如何以编程方式删除数据源。  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include <windows.h>  
#include <odbcinst.h>  
  
int main() {   
   LPCSTR provider = "SQL Server";   // Windows SQL Server Driver  
   LPCSTR provider = "SQL Server";   // Windows SQL Server driver  
   LPCSTR provider2 = "SQL Server Native Client 11.0";   // SQL Server 2012 Native Client driver  
   LPCSTR dsnname = "DSN=data2";  
   BOOL retval = SQLConfigDataSource(NULL, ODBC_REMOVE_DSN, provider, dsnname);  
   std::cout << retval;   // 1 if successful  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置 SQL Server ODBC 驱动程序操作指南主题](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  
