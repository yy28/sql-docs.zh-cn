---
title: SQLConfig数据源（dBASE 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283967"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供特定于 dBASE 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLConfigDataSource**函数用于动态添加、修改或删除数据源，使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|整理顺序|字段排序的顺序。<br /><br /> 序列可以是：ASCII（默认值）或国际。<br /><br /> 这将设置与设置对话框中 **"整理序列"** 相同的选项。|  
|默认DIR|目录的路径规范。|  
|DELETED|对于 dBASE 驱动程序，指定是否可以检索或定位标记为已删除的行。 如果设置为 1，则不显示已删除的行;如果设置为 1，则不显示已删除的行。如果设置为 0，则删除的行将被视为与未删除的行相同。<br /><br /> 这将设置与设置对话框中**显示已删除的行**相同的选项。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置与设置对话框中的 **"说明"** 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|驱动程序 ID|驱动程序的整数 ID。<br /><br /> 21 （dBASE III）<br /><br /> 277 （dBASE IV）<br /><br /> 533 （dBASE 5.0）|  
|FIL|文件类型 dBase III、dBase IV 或 dBase 5|  
|页面超时|指定页面（如果不使用）在删除之前保留在缓冲区中的时间段（以十分之一秒表示）。 默认值为 600 秒（60 秒）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将在设置对话框中设置与**页面超时**相同的选项。|  
|READONLY|TRUE 使文件为只读;FALSE 使文件不只读。<br /><br /> 这将在设置对话框中设置与 **"只读"** 相同的选项。|  
|STATISTICS|对于 dBASE 驱动程序，确定表大小统计信息是否近似。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将在设置对话框中设置与 **"近似行计数"** 相同的选项。|  
|线程|发动机要使用的后台线程数。 此值为 3，无法更改。<br /><br /> 这将设置与设置对话框中的 **"线程"** 相同的选项。|
