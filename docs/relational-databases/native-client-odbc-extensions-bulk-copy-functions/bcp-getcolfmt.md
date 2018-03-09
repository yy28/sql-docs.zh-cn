---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 642290f1093c1f0730417e4bcbed259322c3e630
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  用于查找列格式属性值。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 field  
 要检索其属性的列编号。  
  
 *属性*  
 属性常量之一。  
  
 *pValue*  
 指向要从中检索属性值的缓冲区的指针。  
  
 *cbValue*  
 以字节表示的属性缓冲区的长度。  
  
 *pcbLen*  
 指向属性缓冲区中所返回数据的长度的指针。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 列出列格式属性值[bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)主题。 列的格式属性值设置通过调用**bcp_setcolfmt**函数，与**bcp_getcolfmt**函数用于查找列格式属性值。  
  
 连接到时，可能会看到行为更改[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]（或更高版本） 服务器计算机上，更早版本相比[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 对日期和时间增强功能的支持  
 与使用的类型**BCP_FMT_TYPE**日期/时间类型的属性中指定[增强日期和时间类型 &#40;（OLE DB 和 ODBC）; 的大容量复制更改](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
