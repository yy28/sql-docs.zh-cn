---
title: bcp_done |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
author: rothja
ms.author: jroth
ms.openlocfilehash: cb9b0cbcc927fcd10c2d81b3c5c3d39bb80a8e9b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019575"
---
# <a name="bcp_done"></a>bcp_done
  结束从程序变量进行大容量复制，以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用[bcp_sendrow](bcp-sendrow.md)执行。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 在最后一次调用[bcp_batch](bcp-batch.md)后永久保存的行数; 如果出现错误，则为-1。  
  
## <a name="remarks"></a>备注  
 调用[bcp_sendrow](bcp-sendrow.md)或[bcp_moretext](bcp-moretext.md)最后一次调用后**bcp_done** 。 复制所有数据后，未能调用**bcp_done**会导致错误。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
