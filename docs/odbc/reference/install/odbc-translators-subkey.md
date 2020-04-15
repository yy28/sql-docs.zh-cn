---
title: ODBC 翻译器子键 |微软文档
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
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296217"
---
# <a name="odbc-translators-subkey"></a>ODBC 转换器子项
ODBC 翻译人员子键下的值列出了已安装的译员。 这些值的格式显示在下表中。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|*译者-德茨*|REG_SZ|**安装**|  
  
 *翻译器-desc*名称由转换器开发人员定义。  
  
 例如，假设用户已安装 Microsoft ®代码页转换器和自定义 ASCII 到 EBCDIC 转换器。 ODBC 翻译人员子键下的值可能如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
