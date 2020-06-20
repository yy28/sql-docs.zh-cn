---
title: bcp_columns |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: rothja
ms.author: jroth
ms.openlocfilehash: d634f393b18124e6ae0db753def2c31860f91a74
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019641"
---
# <a name="bcp_columns"></a>bcp_columns
  用于设置在以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为源或目标执行大容量复制时所用的用户文件中找到的列的总数。 可以使用[bcp_setbulkmode](bcp-setbulkmode.md) ，而不是 bcp_columns 和[bcp_colfmt](bcp-colfmt.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
 *nColumns*  
 用户文件中的列的总数。 即使您准备将数据从用户文件大容量复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，并且不想复制用户文件中的所有列，仍必须将*nColumns*设置为用户文件列总数。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 仅当使用有效的文件名调用[bcp_init](bcp-init.md)之后，才能调用此函数。  
  
 仅当您要使用不同于默认设置的用户文件格式时，才应当调用该函数。 有关默认用户文件格式的说明的详细信息，请参阅**bcp_init**。  
  
 调用后 `bcp_columns` ，必须对用户文件中的每个列调用[bcp_colfmt](bcp-colfmt.md)以完全定义自定义文件格式。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
