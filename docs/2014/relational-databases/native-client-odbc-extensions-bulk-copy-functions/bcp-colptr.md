---
title: bcp_colptr |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 38e4b2590bebd09da764e6249e59d32b0c28d356
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705303"
---
# <a name="bcp_colptr"></a>bcp_colptr
  将当前副本的程序变量数据地址设置到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
 *pData*  
 指向要复制的数据的指针。 如果绑定数据类型是大值类型（如 SQLTEXT 或 SQLIMAGE），则*pData*可以为 NULL。 空*pData*表示长数据值将使用[bcp_moretext](bcp-moretext.md)发送到块 SQL Server。  
  
 如果将*pData*设置为 NULL，并且与绑定字段对应的列不是大值类型， **bcp_colptr**会失败。  
  
 有关大值类型的详细信息，请参阅[bcp_bind](bcp-bind.md)**。**  
  
 *idxServerCol*  
 数据复制的目标数据库表中的列的序号位置。 表中的第一列为列 1。 列的序号位置由[SQLColumns](../native-client-odbc-api/sqlcolumns.md)报告。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 使用**bcp_colptr**函数，可以在将数据复制 SQL Server 到[bcp_sendrow](bcp-sendrow.md)时，更改特定列的源数据地址。  
  
 最初，指向用户数据的指针通过调用**bcp_bind**设置。 如果程序变量数据地址在对**bcp_sendrow**的调用之间发生更改，则可以调用**bcp_colptr**来重置指向数据的指针。 对的下一次调用**bcp_sendrow**会将通过调用来寻址的数据发送到**bcp_colptr**。  
  
 对于要修改其数据地址的表中的每一列，都必须有单独的**bcp_colptr**调用。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
