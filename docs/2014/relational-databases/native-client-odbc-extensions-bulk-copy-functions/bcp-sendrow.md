---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e8ef7aa7a4354f5a3fbc334504512b2ee8d131b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688832"
---
# <a name="bcpsendrow"></a>bcp_sendrow
  将一行数据从程序变量发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是大容量复制启用 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 **Bcp_sendrow**函数生成的行从程序变量，并将其发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 然后再调用**bcp_sendrow**，您必须进行到调用[bcp_bind](bcp-bind.md) ，指定包含行数据的程序变量。  
  
 如果**bcp_bind**指定长度可变的长整型数据类型，例如，调用*eDataType* SQLTEXT 和一个非空的参数*pData*参数，则**bcp_sendrow**发送长值，就像任何其他数据类型的操作一样。 如果为，但是， **bcp_bind**具有 NULL *pData*参数， **bcp_sendrow**所有列指定数据都发送到后立即将控制权返回给应用程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 然后，应用程序可以调用[bcp_moretext](bcp-moretext.md)反复将长、 可变长度数据发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，一次一个块。 有关详细信息，请参阅[bcp_moretext](bcp-moretext.md)。  
  
 当**bcp_sendrow**用于大容量复制行从程序变量到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，行时，将提交仅在用户调用[bcp_batch](bcp-batch.md)或[bcp_done](bcp-done.md). 用户可以选择调用**bcp_batch**后每个*n*行或之间的传入数据趋缓时。 如果**bcp_batch**是永远不会调用，会提交这些行时**bcp_done**调用。  
  
 信息的重要更改中大容量复制中的开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，请参阅[执行大容量复制操作&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
