---
title: 国际支持（视觉福克斯Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b0c758bb478ea6a468e6756c3d6f0f52c766f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299967"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>国际性支持（Visual FoxPro ODBC 驱动程序）
微软可视化福克斯Pro ODBC驱动程序支持：  
  
-   双字节字符集 （DBCS）  
  
-   多个整理序列  
  
 整理序列定义存储在 Visual FoxPro 表或数据库中的数据的*排序顺序*。 默认情况下，驱动程序配置为使用支持操作系统语言版本的整理序列。  
  
 有关支持的整理序列的列表，请参阅[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
## <a name="locale"></a>区域设置  
 对应于给定语言和国家/地区的信息集。 区域设置指示特定的设置，如十进制分隔符、日期和时间格式以及字符排序顺序。  
  
## <a name="sort-order"></a>排序顺序 (sort order)  
 排序顺序包含不同*区域设置*的排序规则，允许您正确排序这些语言中的数据。 在 Visual FoxPro 中，当前排序顺序确定字符表达式比较的结果以及记录在索引表或排序表中的显示顺序。
