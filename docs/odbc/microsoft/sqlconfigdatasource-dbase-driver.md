---
title: SQLConfigDataSource （dBASE 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283967"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 dBASE 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 用于动态添加、修改或删除数据源的**SQLConfigDataSource**函数使用以下关键字。  
  
|关键字|说明|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序。<br /><br /> 序列可以是： ASCII （默认值）或国际化。<br /><br /> 这会在 "安装程序" 对话框中设置与**排序顺序**相同的选项。|  
|DEFAULTDIR|目录的路径规范。|  
|DELETED|对于 dBASE 驱动程序，指定是否可以检索或定位已标记为已删除的行。 如果设置为1，则不显示已删除的行;如果设置为0，则将删除的行视为与非删除行相同。<br /><br /> 这会设置与 "设置" 对话框中的 "**显示已删除行**" 相同的选项。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这会在 "设置" 对话框中设置与 "**描述**" 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 21（dBASE III）<br /><br /> 277（dBASE IV）<br /><br /> 533（dBASE 5.0）|  
|FIL|文件类型 dBase III，dBase IV，或 dBase 5|  
|PAGETIMEOUT|指定在删除之前页（如果未使用）保留在缓冲区中的时间段（以十分之一为一秒）。 默认值为600，即十分之一秒（60秒）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这会设置与 "设置" 对话框中**页面超时**相同的选项。|  
|READONLY|若要使文件为只读，则为 TRUE;如果设置为 FALSE，则使文件不为只读。<br /><br /> 这会在 "设置" 对话框中设置与 "**只读**" 相同的选项。|  
|STATISTICS|对于 dBASE 驱动程序，确定表大小统计信息是否近似。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这会设置与 "设置" 对话框中的 "**近似行计数**" 相同的选项。|  
|线程|引擎要使用的后台线程数。 此值为3，无法更改。<br /><br /> 这会设置与 "设置" 对话框中的**线程**相同的选项。|
