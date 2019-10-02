---
title: 大容量复制文本和图像数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5243c862e07ad8b4f5a0b3b33ea292cecc1cb0a9
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707901"
---
# <a name="bulk-copying-text-and-image-data"></a>大容量复制文本和图像数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)函数大容量复制较大的**text**、 **ntext**和**image**值。 为**text**、 **ntext**或**image**列编写[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) ，并将*pData*指针设置为 NULL，指示将使用**bcp_moretext**提供数据。 务必指定为每个大容量复制行中的每个**text**、 **ntext**或**image**列提供的数据的准确长度。 如果列的数据长度不同于[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)中指定的列长度，请使用[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)将长度设置为正确的值。 [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)发送所有非**文本**、非**ntext**和非**图像**数据;然后，调用**bcp_moretext**以单独的单位发送**text**、 **ntext**或**image**数据。 大容量复制函数确定当通过**bcp_moretext**发送的数据的长度与最新 bcp_collen 中指定的长度相等时，已发送当前**text**、 **ntext**或**image**列的所有数据。或**bcp_bind**。  
  
 **bcp_moretext**没有用于标识列的参数。 如果一行中有多个**text**、 **ntext**或**image**列， **bcp_moretext**将对以具有最低序号的列开头的**text**、 **ntext**或**image**列进行操作，转到序号最高的列。 当发送的数据的长度与当前列的最新**bcp_collen**或**bcp_bind**中指定的长度相等时， **bcp_moretext**从一列转到下一列。  
  
## <a name="see-also"></a>请参阅  
 [正在执行大容量&#40;复制操作 ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
