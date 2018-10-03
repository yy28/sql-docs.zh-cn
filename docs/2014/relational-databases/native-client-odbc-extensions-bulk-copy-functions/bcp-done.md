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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0326330e3d2052e8e997a293f666a8fc725391b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058997"
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
  
## <a name="remarks"></a>备注  
 调用**bcp_done**到最后一次调用后[bcp_sendrow](bcp-sendrow.md)或[bcp_moretext](bcp-moretext.md)。 调用失败**bcp_done**后复制所有数据将导致错误。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
