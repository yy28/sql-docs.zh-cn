---
title: bcp_done |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 630762fc74a9c1c71d24d40a1ba22bf6627a0d0c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414716"
---
# <a name="bcpdone"></a>bcp_done
  结束从到程序变量大容量复制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是大容量复制启用 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 永久保存到的最后一个调用后的行数[bcp_batch](bcp-batch.md)或发生错误时为-1。  
  
## <a name="remarks"></a>Remarks  
 调用**bcp_done**到最后一次调用后[bcp_sendrow](bcp-sendrow.md)或[bcp_moretext](bcp-moretext.md)。 调用失败**bcp_done**后复制所有数据将导致错误。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
