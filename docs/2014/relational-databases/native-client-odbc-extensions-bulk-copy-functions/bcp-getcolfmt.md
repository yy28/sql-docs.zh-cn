---
title: bcp_getcolfmt |Microsoft 文档
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
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1dcae7d7934221e1df720869d09aa6abcf958c04
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018184"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
  用于查找列格式属性值。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_getcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbvalue,  
INT*   
pcbLen  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 field  
 要检索其属性的列编号。  
  
 property  
 属性常量之一。  
  
 *pValue*  
 指向要从中检索属性值的缓冲区的指针。  
  
 *cbValue*  
 以字节表示的属性缓冲区的长度。  
  
 *pcbLen*  
 指向属性缓冲区中所返回数据的长度的指针。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 列出列格式属性值[bcp_setcolfmt](bcp-setcolfmt.md)主题。 列的格式属性值设置通过调用**bcp_setcolfmt**函数，与**bcp_getcolfmt**函数用于查找列格式属性值。  
  
 连接到时，可能会看到行为更改[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]（或更高版本） 服务器计算机上，更早版本相比[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 对日期和时间增强功能的支持  
 与使用的类型`BCP_FMT_TYPE`日期/时间类型的属性中指定[增强日期和时间类型的大容量复制更改&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  