---
title: 时间和日期功能（可视化福克斯Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86260f8e7245bed15122d4dbfc4649131674e17f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303058"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>时间和日期函数（Visual FoxPro ODBC 驱动程序）
下表列出了 Visual FoxPro ODBC 驱动程序支持的 ODBC 时间和日期函数;当相同函数的 Visual FoxPro 语法与 ODBC 语法不同时，将列出 Visual FoxPro 等效项。  
  
|ODBC 语法|可视化 FoxPro 语法|  
|------------------|---------------------------|  
|CURDATE *（ ）*|日期 *（ ）*|  
|CURTIME *（ ）*|时间 *（ ）*|  
|天名 *（date_exp）*|CDOW *（date_exp）*|  
|一月 *（date_exp日）*|日 *（ ）*|  
|小时 *（time_exp）*||  
|分钟 *（time_exp）*||  
|月 *（time_exp）*||  
|月名 *（date_exp）*|CMONTH *（date_exp）*|  
|现在 *（ ）*|日期时间 *（ ）*|  
|秒 *（time_exp）*|SEC *（time_exp）*|  
|周 *（date_exp）*||  
|年份 *（date_exp）*||  
  
 不支持以下时间和日期函数：  
  
 一天 *（date_exp）*  
  
 *（date_exp）*  
  
 时间戳（*间隔、integer_exp、timestamp_exp）*  
  
 时间戳 *（间隔、timestamp_exp1、timestamp_exp2）*  
  
## <a name="odbc-escape-sequences"></a>ODBC 转义序列  
 驱动程序还支持日期和时间戳数据的 ODBC 转义序列。 转义子句语法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 在此语法中 **，d**指示*值*是*yyyy-mm-dd*格式的日期 **，ts**表示*值*是*yyyy-mm-dhh：mm：ss*中的时间戳 。*f...* 格式。 日期和时间戳数据的速记语法如下所示：  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如，以下每个语句都使用受支持的 SQL UPDATE 命令中的日期和时间戳速记语法更新 ALLTYPES 表：  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>备注  
 有关转义序列的详细信息，请参阅*ODBC 程序员参考*[中的 ODBC 中的转义序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
