---
title: bcp_batch |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e01952fbe3fcba497544b9defd94044bdf06bf09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027269"
---
# <a name="bcpbatch"></a>bcp_batch
  提交所有行以前大容量复制从程序变量并发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 保存到的最后一个调用后的行数**bcp_batch**，则为-1 发生错误。  
  
## <a name="remarks"></a>Remarks  
 大容量复制批处理定义事务。 当应用程序使用[bcp_bind](bcp-bind.md)和**bcp_sendrow**大容量复制行从程序变量向 SQL Server 表，行时，将提交仅在程序调用**bcp_batch**或[bcp_done](bcp-done.md)。  
  
 你可以调用**bcp_batch**后每个*n*行或减缓 （如下所示的遥测应用程序） 的传入数据中时。 如果应用程序不会调用**bcp_batch**的大容量复制行进行提交时，才**bcp_done**调用。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  