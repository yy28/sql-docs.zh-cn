---
title: "bcp_sendrow |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_sendrow
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e332dbcf96d58b867029a3a5ec4f7be950b1992d
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2018
---
# <a name="bcpsendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  将一行数据从程序变量发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 **Bcp_sendrow**函数生成从程序变量的行，并将其发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 之前调用**bcp_sendrow**，您必须对进行调用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)以指定包含行数据的程序变量。  
  
 如果**bcp_bind**指定 long、 可变长度数据类型，例如，调用*eDataType* SQLTEXT 和非 NULL 参数*pData*参数、 **bcp_sendrow**发送整个数据值，就像任何其他数据类型。 如果是，但是， **bcp_bind**具有 NULL *pData*参数， **bcp_sendrow**将控制返回给应用程序，所有列与指定的数据都发送到后立即[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 然后，应用程序可以调用[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)重复以 long、 可变长度数据发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，一次一个块。 有关详细信息，请参阅[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)。  
  
 当**bcp_sendrow**用于大容量复制行从程序变量到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，行提交只有当有用户调用[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)或[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). 用户可以选择调用**bcp_batch**后每个 *n* 行或在传入数据的时间段之间没有减缓时。 如果**bcp_batch**是永远不会调用，行时，将提交**bcp_done**调用。  
  
 璝惠了重大更改正在大容量复制中开始的[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，请参阅[执行大容量复制操作 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
