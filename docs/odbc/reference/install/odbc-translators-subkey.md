---
description: ODBC 转换器子项
title: ODBC 转换器子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46308518f1f806cea21bbb824312d5269f8b61e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499710"
---
# <a name="odbc-translators-subkey"></a>ODBC 转换器子项
ODBC 转换器子项下的值列出了已安装的转换器。 下表显示了这些值的格式。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|*转换器-desc*|REG_SZ|**已安装**|  
  
 *转换器-desc*名称由 translator 开发人员定义。  
  
 例如，假设用户已安装 Microsoft®代码页转换器和自定义的 ASCII 到 EBCDIC 转换器。 ODBC 转换器子项下的值如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
