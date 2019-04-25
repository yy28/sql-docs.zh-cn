---
title: 国际支持 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50d65520e74a4e11bada88795fedc0b2f2e82628
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471040"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>国际性支持（Visual FoxPro ODBC 驱动程序）
Microsoft Visual FoxPro ODBC 驱动程序支持：  
  
-   双字节字符集 (DBCS)  
  
-   多个排序规则序列  
  
 排序顺序定义*排序顺序*Visual FoxPro 表或数据库中存储的数据。 默认情况下，该驱动程序配置为使用支持的操作系统的语言版本的排序规则序列。  
  
 有关受支持的排序规则序列的列表，请参阅[设置 COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
## <a name="locale"></a>区域设置 (locale)  
 对应于给定的语言和国家/地区的信息集。 区域设置指示特定设置，例如十进制分隔符、 日期和时间格式，以及字符排序顺序。  
  
## <a name="sort-order"></a>排序顺序 (sort order)  
 排序顺序合并不同的排序规则*区域设置*的使您可以正确地对这些语言中的数据进行排序。 Visual FoxPro 中当前的排序顺序确定的字符表达式比较和在其中记录的显示的顺序中编制索引或排序表的结果。
