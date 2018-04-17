---
title: 时间和日期函数 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5ba661df5c57c9611164889126eab9572743c8e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>时间和日期函数 （Visual FoxPro ODBC 驱动程序）
下表列出了 Visual FoxPro ODBC 驱动程序; 支持的 ODBC 的日期和时间函数当相同的功能的 Visual FoxPro 语法不同于 ODBC 语法，将列等效 Visual FoxPro。  
  
|ODBC 语法|Visual FoxPro 语法|  
|------------------|---------------------------|  
|CURDATE*（)*|日期*（)*|  
|CURTIME*（)*|时间*（)*|  
|DAYNAME*(date_exp)*|CDOW*(date_exp)*|  
|DAYOFMONTH (*date_exp)*|天*（)*|  
|小时*(time_exp)*||  
|分钟*(time_exp)*||  
|月*(time_exp)*||  
|月份名称*(date_exp)*|CMONTH*(date_exp)*|  
|现在*（)*|DATETIME*（)*|  
|第二个*(time_exp)*|每秒*(time_exp)*|  
|周*(date_exp)*||  
|年*(date_exp)*||  
  
 不支持以下的时间和日期函数：  
  
 DAYOFYEAR *(date_exp)*  
  
 季度*(date_exp)*  
  
 TIMESTAMPADD *（间隔、 integer_exp、 timestamp_exp）*  
  
 TIMESTAMPDIFF *（间隔、 timestamp_exp1、 timestamp_exp2）*  
  
## <a name="odbc-escape-sequences"></a>ODBC 转义序列  
 该驱动程序还支持 ODBC 转义序列的日期和时间戳的数据。 Escape 子句语法如下所示：  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 在此语法中， **d**指示*值*是中的某个日期*yyyy-月-日*格式和**ts**指示*值*是时间戳*yyyy mm dd hh: mm:*[。*f...*] 格式。 日期和时间戳数据速记形式语法如下所示：  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 例如，每个以下语句通过在支持的 SQL UPDATE 命令中使用的日期和时间戳速记语法来更新 ALLTYPES 表：  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>注释  
 有关转义序列的详细信息，请参阅[ODBC 中的转义序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中*ODBC 程序员参考*。
