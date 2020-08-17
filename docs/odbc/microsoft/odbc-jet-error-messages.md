---
description: ODBC Jet 错误消息
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19f7d4b00c9e6b206ecd563083c0fcf16ced55e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340713"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 错误消息
对于数据源中发生的错误，ODBC 驱动程序将返回一个由 ODBC 文件库返回的错误消息。 对于 ODBC 驱动程序或驱动程序管理器中发生的错误，驱动程序将基于与 SQLSTATE 关联的文本返回一条错误消息。  
  
 错误消息具有以下格式：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 括号中的前缀 ( [] ) 标识错误的位置。 当驱动程序管理器中出现错误时，不提供 *数据源* 。 当数据源中出现错误时，[*供应商*] 和 [*ODBC 组件*] 前缀将标识从数据源接收到错误的 ODBC 组件的供应商和名称。  
  
 下表显示了驱动程序管理器和驱动程序 ISAM 返回的错误消息：  
  
|错误消息|错误位置|  
|-------------------|--------------------|  
|微软[ODBC 驱动程序管理器] *消息文本*|驱动程序管理器 ( # A0) |  
|微软[ODBC *驱动程序名称*]*消息文本*|驱动程序 ISAM (参阅驱动程序 ISAMs) |
