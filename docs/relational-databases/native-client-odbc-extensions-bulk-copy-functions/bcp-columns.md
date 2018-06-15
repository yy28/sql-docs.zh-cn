---
title: bcp_columns |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_columns
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f0509823206c7e2b0062bd3587eb31aeee982369
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948622"
---
# <a name="bcpcolumns"></a>bcp_columns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  用于设置在以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为源或目标执行大容量复制时所用的用户文件中找到的列的总数。 [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)可代替 bcp_columns 和[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_columns (  
        HDBC hdbc,  
        INT nColumns);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 *nColumns*  
 用户文件中的列的总数。 即使你准备从大容量复制数据的用户文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表并不打算将所有列中的用户文件的都复制，你仍必须设置*nColumns*用户文件列的总数。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 可以调用此函数后，才[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)已调用具有有效的文件名称。  
  
 仅当您要使用不同于默认设置的用户文件格式时，才应当调用该函数。 有关默认的用户文件格式的说明的详细信息，请参阅**bcp_init**。  
  
 在调用**bcp_columns**，必须调用[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)要完整地定义自定义文件格式的用户文件中每一列。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
