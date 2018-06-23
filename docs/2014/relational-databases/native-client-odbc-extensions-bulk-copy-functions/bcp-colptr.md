---
title: bcp_colptr |Microsoft 文档
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
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c0fa867ec82520f1dcc0def040d7a8edf8a2a713
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126528"
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
 为大容量复制启用 ODBC 连接句柄。  
  
 *pData*  
 指向要复制的数据的指针。 如果绑定的数据类型是较大的值类型 （如 SQLTEXT 或 SQLIMAGE） *pData*可以为 NULL。 NULL *pData*指示长整型数据值将发送到 SQL Server 中使用的区块[bcp_moretext](bcp-moretext.md)。  
  
 如果*pData*设置为 NULL，且列对应于绑定的字段不是较大的值类型， **bcp_colptr**失败。  
  
 有关大型值类型的详细信息，请参阅[bcp_bind](bcp-bind.md)**。**  
  
 *idxServerCol*  
 数据复制的目标数据库表中的列的序号位置。 表中的第一列为列 1。 列的序号位置报告的[SQLColumns](../native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 **Bcp_colptr**函数使你可以将某个特定列的源数据的地址更改时将数据复制到 SQL Server [bcp_sendrow](bcp-sendrow.md)。  
  
 最初，通过调用设置指向用户数据的指针**bcp_bind**。 如果程序变量数据地址发生更改之间调用**bcp_sendrow**，可以调用**bcp_colptr**重置的数据的指针。 下次调用**bcp_sendrow**将数据发送到调用发送**bcp_colptr**。  
  
 必须有一个单独**bcp_colptr**其数据解决你的表中每个列调用想要修改。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  