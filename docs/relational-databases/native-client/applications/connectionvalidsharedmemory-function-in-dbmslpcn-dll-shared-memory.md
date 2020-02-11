---
title: ConnectionValidSharedMemory dbmslpcn
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c64fe0020ca6c406cadd5b5b71ade1641919a81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244203"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Dbmslpcn.dll 共享内存中的 ConnectionValidSharedMemory 函数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  函数确定是否已安装并激活 SQL Server 共享内存。  
  
## <a name="syntax"></a>语法  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>parameters  
 *szServerName*  
  
-   类型： **char\* **  
  
-   SQL server 的名称。  
  
## <a name="return-value"></a>返回值  
 类型： **BOOL**  
  
 如果无效，则返回 0;否则返回非零值。  
  
  
