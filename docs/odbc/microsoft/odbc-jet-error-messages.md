---
title: "ODBC Jet 错误消息 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0fad2aab1020cb7a56c00a2b78c1d2c46a41c422
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 错误消息
对于在数据源中发生的错误，ODBC 驱动程序返回错误消息返回到该 ODBC 文件库。 对于 ODBC 驱动程序或驱动程序管理器中发生的错误，该驱动程序将返回一条错误消息基于文本与 SQLSTATE 关联。  
  
 错误消息具有以下格式：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 方括号 ([]) 中的前缀标识错误的位置。 在驱动程序管理器中，发生错误时*数据源*未提供。 在数据源中发生错误时 [*供应商*] 和 [*ODBC 组件*] 前缀确定的供应商和从数据源收到了错误的 ODBC 组件名称。  
  
 下表显示由驱动程序管理器和驱动程序 ISAM 返回的错误消息：  
  
|错误消息|错误位置|  
|-------------------|--------------------|  
|[Microsoft][ODBC 驱动程序管理器]*消息文本*|驱动程序管理器 (所用的 Odbc32.dll)|  
|[Microsoft][ODBC*驱动程序名称*]*消息文本*|驱动程序 ISAM （请参阅驱动程序 ISAMs）|

