---
title: bcp_batch |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_batch
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee208e08edd8c68e204f8ac531758850366e8687
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407496"
---
# <a name="bcpbatch"></a>bcp_batch
  提交所有以前大容量复制从程序变量和行发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是大容量复制启用 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 保存到的最后一个调用后的行数**bcp_batch**，则发生错误时为-1。  
  
## <a name="remarks"></a>Remarks  
 大容量复制批处理定义事务。 当应用程序使用[bcp_bind](bcp-bind.md)并**bcp_sendrow**大容量复制行从程序变量到 SQL Server 表，会提交这些行仅当程序调用**bcp_batch**或[bcp_done](bcp-done.md)。  
  
 您可以调用**bcp_batch**后每个*n*行中 （如下所示的遥测应用程序） 的传入数据趋缓时。 如果应用程序不会调用**bcp_batch**才提交大容量复制行时，才**bcp_done**调用。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
