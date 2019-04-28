---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db8b433652829b16890552a70bd1e0d08d1c1bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689086"
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
 是大容量复制启用 ODBC 连接句柄。  
  
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
  
## <a name="remarks"></a>备注  
 列格式属性值中列出[bcp_setcolfmt](bcp-setcolfmt.md)主题。 通过调用设置列格式属性值**bcp_setcolfmt**函数，并**bcp_getcolfmt**函数用于查找列格式属性值。  
  
 连接到时，可能会看到行为更改[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]（或更高版本） 服务器计算机上，与之前相比[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 对日期和时间增强功能的支持  
 与使用的类型`BCP_FMT_TYPE`日期/时间类型的属性中指定的那样[大容量复制更改的增强的日期和时间类型&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
