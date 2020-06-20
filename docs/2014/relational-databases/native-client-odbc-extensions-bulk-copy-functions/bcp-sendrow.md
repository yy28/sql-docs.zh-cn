---
title: bcp_sendrow |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c45e87fdd8e00e9456718c4c9c8160c22bac03a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019375"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
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
 是启用大容量复制的 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 **Bcp_sendrow**函数从程序变量生成行并将其发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 在调用**bcp_sendrow**之前，必须调用[bcp_bind](bcp-bind.md)以指定包含行数据的程序变量。  
  
 如果**bcp_bind**指定长度可变的长整型数据类型（例如，SQLTEXT 的*eDataType*参数和非空的*pData*参数），则**bcp_sendrow**发送整型值，正如对任何其他数据类型的情况一样。 但是，如果**bcp_bind**具有 NULL *pData*参数，则**bcp_sendrow**会在将具有指定数据的所有列发送到之后立即将控制权返回给应用程序 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 然后，应用程序可以反复调用[bcp_moretext](bcp-moretext.md)将长的可变长度数据发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，一次发送一个块区。 有关详细信息，请参阅[bcp_moretext](bcp-moretext.md)。  
  
 当使用**bcp_sendrow**将行从程序变量大容量复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中时，仅当用户调用[bcp_batch](bcp-batch.md)或[bcp_done](bcp-done.md)时才提交行。 用户可以选择每*n*行调用一次**bcp_batch** ，或在传入数据的时间段之间进行趋缓。 如果永远不会调用**bcp_batch** ，则在调用**bcp_done**时将提交行。  
  
 有关从开始大容量复制的重大更改的信息 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，请参阅[&#40;ODBC&#41;执行大容量复制操作](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
