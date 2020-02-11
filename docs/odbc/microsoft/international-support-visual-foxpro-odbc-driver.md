---
title: 国际性支持（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.openlocfilehash: e987c224f2d716fcab3bf898b1cb276e922e48ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085505"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>国际性支持（Visual FoxPro ODBC 驱动程序）
Microsoft Visual FoxPro ODBC 驱动程序支持：  
  
-   双字节字符集（DBCS）  
  
-   多个排序序列  
  
 排序规则定义存储在 Visual FoxPro 表或数据库中的数据的*排序顺序*。 默认情况下，该驱动程序配置为使用支持您的操作系统语言版本的排序规则。  
  
 有关支持的排序规则的列表，请参阅[设置整理](../../odbc/microsoft/set-collate-command.md)。  
  
## <a name="locale"></a>区域设置  
 对应于给定语言和国家/地区的信息集。 区域设置指示特定的设置，如小数分隔符、日期和时间格式以及字符排序顺序。  
  
## <a name="sort-order"></a>排序顺序 (sort order)  
 排序顺序合并了不同*区域设置*的排序规则，从而使您能够正确地对这些语言中的数据进行排序。 在 Visual FoxPro 中，当前排序顺序确定了字符表达式比较的结果，以及记录在索引或排序表中的显示顺序。
