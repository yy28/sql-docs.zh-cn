---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e7109a6f1b88cf7639b2fc823ce0c5f14d05002
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673235"
---
# <a name="odbc-translators-subkey"></a>ODBC 转换器子项
ODBC 转换器子项下的值列出已安装的转换器。 下表中显示这些值的格式。  
  
|“属性”|数据类型|data|  
|----------|---------------|----------|  
|*转换器 desc*|REG_SZ|**安装**|  
  
 *转换器 desc*转换器开发人员通过定义名称。  
  
 例如，假设用户已经安装了 Microsoft® 代码页 Translator 和自定义 ASCII 到 EBCDIC 转换器。 ODBC 转换器子项下的值可能按如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
