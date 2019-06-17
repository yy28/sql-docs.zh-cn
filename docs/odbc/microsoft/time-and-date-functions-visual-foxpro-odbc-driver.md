---
title: 时间和日期函数 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf8e7552faf9567dab25ee3dc5b7b293034faef0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632767"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>时间和日期函数（Visual FoxPro ODBC 驱动程序）
下表列出了支持的 Visual FoxPro ODBC 驱动程序; ODBC 日期和时间函数在相同的功能的 Visual FoxPro 语法与 ODBC 语法不同，会列出等效 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|CURDATE *（)*|日期 *（)*|  
|CURTIME *（)*|时间 *（)*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH(*date_exp)*|一天 *（)*|  
|HOUR *(time_exp)*||  
|MINUTE *(time_exp)*||  
|MONTH *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|现在 *（)*|DATETIME *( )*|  
|SECOND *(time_exp)*|SEC *(time_exp)*|  
|WEEK *(date_exp)*||  
|YEAR *(date_exp)*||  
  
 不支持以下日期和时间函数：  
  
 DAYOFYEAR *(date_exp)*  
  
 QUARTER *(date_exp)*  
  
 TIMESTAMPADD *（时间间隔，integer_exp，timestamp_exp）*  
  
 TIMESTAMPDIFF *(interval, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC 转义序列  
 该驱动程序还支持 ODBC 转义序列的日期和时间戳数据。 Escape 子句语法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 在此语法中， **d**指示*值*是中的某个日期*年-月-日*格式和**ts**指示*值*是在一个时间戳*年-月-日： 分： 秒*[。*f...* ] 格式。 日期和时间戳数据的速记语法如下所示：  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如，以下语句的每个受支持的 SQL UPDATE 命令中使用日期和时间戳速记形式语法更新 ALLTYPES 表：  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>备注  
 有关转义序列的详细信息，请参阅[ODBC 中的转义序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中*ODBC 程序员参考*。
