---
title: bcp_batch |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62631381"
---
# <a name="bcp_batch"></a>bcp_batch
  将以前从程序变量大容量复制的所有行提交[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
## <a name="returns"></a>返回  
 在最后一次调用**bcp_batch**之后保存的行数; 如果出现错误，则为-1。  
  
## <a name="remarks"></a>备注  
 大容量复制批处理定义事务。 当应用程序使用[bcp_bind](bcp-bind.md)和**bcp_sendrow**将行从程序变量大容量复制到 SQL Server 表时，只在程序调用**bcp_batch**或[bcp_done](bcp-done.md)时才提交行。  
  
 可以在每*n*行调用一次**bcp_batch** ，或在传入数据中有趋缓时调用（如在遥测应用程序中）。 如果应用程序不调用**bcp_batch**仅当调用**bcp_done**时才提交大容量复制的行。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
