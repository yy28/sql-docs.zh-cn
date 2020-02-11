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
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093944"
---
# <a name="odbc-translators-subkey"></a>ODBC 转换器子项
ODBC 转换器子项下的值列出了已安装的转换器。 下表显示了这些值的格式。  
  
|名称|数据类型|data|  
|----------|---------------|----------|  
|*转换器-desc*|REG_SZ|**随**|  
  
 *转换器-desc*名称由 translator 开发人员定义。  
  
 例如，假设用户已安装 Microsoft®代码页转换器和自定义的 ASCII 到 EBCDIC 转换器。 ODBC 转换器子项下的值如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
