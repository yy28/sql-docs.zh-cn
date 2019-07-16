---
title: SQLConfigDataSource (dBASE Driver) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 569a83110d7d5a3cd25eed8f68753d13793f8b10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054097"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供 dBASE 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序的序列。<br /><br /> 序列可以是：ASCII （默认值） 或国际。<br /><br /> 这将设置为相同的选项**排序规则序列**中设置的对话框。|  
|DEFAULTDIR|所指定的路径的目录。|  
|DELETED|对于 dBASE 驱动程序，指定可以检索或位于已标记为已删除的行。 如果未显示设置为 1，已删除的行;如果设置为 0，已删除的行是相同视为非删除行。<br /><br /> 这将设置为相同的选项**显示删除的行**中设置的对话框。|  
|DESCRIPTION|数据源中的数据说明。<br /><br /> 这将设置为相同的选项**说明**中设置的对话框。|  
|DRIVER|路径规范，以驱动程序 DLL。|  
|DRIVERID|驱动程序的一个整数 ID。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|文件键入 dBase III、 dBase IV 或 dBase 5|  
|PAGETIMEOUT|指定时间，的段中 （如果不使用） 会保留一页在缓冲区中被删除前一秒的十分之几。 默认值为 600 秒 （60 秒） 的十分之几秒。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**页超时**中设置的对话框。|  
|READONLY|若要使文件只读的;如果为 FALSE，则若要使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**中设置的对话框。|  
|STATISTICS|对于 dBASE 驱动程序，确定是否近似表大小统计信息。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**近似行计数**中设置的对话框。|  
|线程|要使用的引擎的后台线程数。 此值为 3，不能更改。<br /><br /> 这将设置为相同的选项**线程**中设置的对话框。|
