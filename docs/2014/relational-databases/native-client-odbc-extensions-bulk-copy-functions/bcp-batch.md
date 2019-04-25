---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c41e8d90adc8ff6eb2058feebe3f33c10edbfa92
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631381"
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
  
## <a name="remarks"></a>备注  
 大容量复制批处理定义事务。 当应用程序使用[bcp_bind](bcp-bind.md)并**bcp_sendrow**大容量复制行从程序变量到 SQL Server 表，会提交这些行仅当程序调用**bcp_batch**或[bcp_done](bcp-done.md)。  
  
 您可以调用**bcp_batch**后每个*n*行中 （如下所示的遥测应用程序） 的传入数据趋缓时。 如果应用程序不会调用**bcp_batch**才提交大容量复制行时，才**bcp_done**调用。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
