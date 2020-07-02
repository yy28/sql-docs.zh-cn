---
title: ConnectionValidSharedMemory dbmslpcn.dll
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43a4bdb3b5e20246fc464d347710fb57f0584f0c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85657495"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Dbmslpcn.dll 共享内存中的 ConnectionValidSharedMemory 函数
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  函数确定是否已安装并激活 SQL Server 共享内存。  
  
## <a name="syntax"></a>语法  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>参数  
 *szServerName*  
  
-   类型： **char \* **  
  
-   SQL server 的名称。  
  
## <a name="return-value"></a>返回值  
 类型： **BOOL**  
  
 如果无效，则返回 0;否则返回非零值。  
  
  
