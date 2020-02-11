---
title: bcp_batch |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_batch
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f435b0ba0d7474867af20aea1d59bd6118035623
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783230"
---
# <a name="bcp_batch"></a>bcp_batch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  将以前从程序变量大容量复制的所有行提交[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBINT bcp_batch (HDBC  
        hdbc);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 在最后一次调用**bcp_batch**之后保存的行数; 如果出现错误，则为-1。  
  
## <a name="remarks"></a>备注  
 大容量复制批处理定义事务。 当应用程序使用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和**bcp_sendrow**将行从程序变量大容量复制到 SQL Server 表时，只在程序调用**bcp_batch**或[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)时才提交行。  
  
 可以在每*n*行调用一次**bcp_batch** ，或在传入数据中有趋缓时调用（如在遥测应用程序中）。 如果应用程序不调用**bcp_batch**仅当调用**bcp_done**时才提交大容量复制的行。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
