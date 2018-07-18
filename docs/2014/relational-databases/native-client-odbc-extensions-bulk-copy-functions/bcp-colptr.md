---
title: bcp_colptr |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0c548a1decd7410cd1cbc8df3ee68126e62ca25
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413566"
---
# <a name="bcpcolptr"></a>bcp_colptr
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
 是大容量复制启用 ODBC 连接句柄。  
  
 *pData*  
 指向要复制的数据的指针。 如果绑定的数据类型是大值类型 （如 SQLTEXT 或 SQLIMAGE）， *pData*可以为 NULL。 为空*pData*指示长数据值将发送到 SQL Server 中使用的区块[bcp_moretext](bcp-moretext.md)。  
  
 如果*pData*设置为 NULL，并且列与绑定字段对应的大值类型，不是**bcp_colptr**失败。  
  
 有关大值类型的详细信息，请参阅[bcp_bind](bcp-bind.md)**。**  
  
 *idxServerCol*  
 数据复制的目标数据库表中的列的序号位置。 表中的第一列为列 1。 报告列的序号位置[SQLColumns](../native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 **Bcp_colptr**功能，您可以更改特定列的源数据的地址，将数据复制到与 SQL Server 时[bcp_sendrow](bcp-sendrow.md)。  
  
 最初，通过调用设置的用户数据指针**bcp_bind**。 如果程序变量数据地址发生更改调用之间**bcp_sendrow**，可以调用**bcp_colptr**重置的数据的指针。 下次调用**bcp_sendrow**发送到调用的数据**bcp_colptr**。  
  
 必须单独**bcp_colptr**要修改其数据地址的表中的每列的调用。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
