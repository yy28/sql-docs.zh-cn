---
title: 大容量复制文本和图像数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 03d77ce1a4526cee78431def0251329111433aac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705828"
---
# <a name="bulk-copying-text-and-image-data"></a>大容量复制文本和图像数据
  使用[bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)函数大容量复制较大的**text**、 **ntext**和**image**值。 为**text**、 **ntext**或**image**列编写[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) ，并将*pData*指针设置为 NULL，指示将使用**bcp_moretext**提供数据。 务必指定为每个大容量复制行中的每个**text**、 **ntext**或**image**列提供的数据的准确长度。 如果列的数据长度与[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)中指定的列长度不同，则使用[bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)将长度设置为正确的值。 [Bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)发送所有非**文本**、非**ntext**和非**图像**数据;然后，调用**bcp_moretext**以单独的单位发送**text**、 **ntext**或**image**数据。 大容量复制函数确定当通过**bcp_moretext**发送的数据的长度之和等于最新**bcp_collen**或**bcp_bind**中指定的长度时，已发送当前**text**、 **ntext**或**image**列的所有数据。  
  
 **bcp_moretext**没有用于标识列的参数。 如果一行中有多个**text**、 **ntext**或**image**列， **bcp_moretext**将对以具有最低序号的列执行运算，并使用最大序号的列执行对**text**、 **ntext**或**image**列的运算。 当发送的数据的长度与最新的 bcp_collen 中指定的长度等于当前列的最新**bcp_collen**或**bcp_bind**时， **bcp_moretext**将从一列转到下一列。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;执行大容量复制操作](performing-bulk-copy-operations-odbc.md)  
  
  
