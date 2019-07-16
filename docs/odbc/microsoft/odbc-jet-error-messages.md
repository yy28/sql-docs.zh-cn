---
title: ODBC Jet 错误消息 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85e0f9a8bc7015a0ad5b12ce46a6c94ab31ca43c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915815"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 错误消息
对于数据源中出现的错误，ODBC 驱动程序返回错误消息返回到该 ODBC 文件库。 对于 ODBC 驱动程序或驱动程序管理器中发生的错误，的返回一条错误消息基于文本的驱动程序与关联的 SQLSTATE。  
  
 错误消息具有以下格式：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 方括号 ([]) 中的前缀标识错误的位置。 在驱动程序管理器中，发生错误时*数据源*未提供。 在数据源中发生错误时 [*供应商*] 和 [*ODBC 组件*] 前缀标识供应商和从数据源收到了错误的 ODBC 组件名称。  
  
 下表显示了由驱动程序管理器和驱动程序 ISAM 返回的错误消息：  
  
|错误消息|错误位置|  
|-------------------|--------------------|  
|[Microsoft][ODBC 驱动程序管理器]*消息文本*|驱动程序管理器 (所用的 Odbc32.dll)|  
|[Microsoft][ODBC *driver-name*]*message-text*|驱动程序 ISAM （请参阅驱动程序 ISAMs）|
