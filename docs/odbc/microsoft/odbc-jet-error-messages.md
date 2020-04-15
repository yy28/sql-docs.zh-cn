---
title: ODBC 喷射错误消息 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fa6e672b69c7791e66dc3919e6fcd22b7c3de7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293107"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 错误消息
对于数据源中发生的错误，ODBC 驱动程序将返回由 ODBC 文件库返回的错误消息。 对于在 ODBC 驱动程序或驱动程序管理器中发生的错误，驱动程序会返回一条错误消息，该错误消息基于与 SQLSTATE 关联的文本。  
  
 错误消息具有以下格式：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 括号 （* +） 中的前缀标识错误的位置。 当驱动程序管理器中发生错误时，不会给出*数据源*。 当数据源中发生错误时， [*供应商*] 和 [*ODBC- 组件*] 前缀标识从数据源接收错误的 ODBC 组件的供应商和名称。  
  
 下表显示了驱动程序管理器和驱动程序 ISAM 返回的错误消息：  
  
|错误消息|错误位置|  
|-------------------|--------------------|  
|[微软][ODBC 驱动程序管理器]*消息文本*|驾驶员管理器（Odbc32.dll）|  
|[微软][ODBC*驱动程序名称*]*消息文本*|驱动程序 ISAM（请参阅驱动程序 ISAM）|
