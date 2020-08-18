---
description: SQLConfigDataSource（dBASE 驱动程序）
title: SQLConfigDataSource (dBASE 驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 23e734c5aafc903e210eea18f002f4c5e8d7a456
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411953"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 dBASE 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 用于动态添加、修改或删除数据源的 **SQLConfigDataSource** 函数使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序。<br /><br /> 序列可为： (默认) 或国际的 ASCII。<br /><br /> 这会在 "安装程序" 对话框中设置与 **排序顺序** 相同的选项。|  
|DEFAULTDIR|目录的路径规范。|  
|DELETED|对于 dBASE 驱动程序，指定是否可以检索或定位已标记为已删除的行。 如果设置为1，则不显示已删除的行;如果设置为0，则将删除的行视为与非删除行相同。<br /><br /> 这会设置与 "设置" 对话框中的 " **显示已删除行** " 相同的选项。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这会在 "设置" 对话框中设置与 " **描述** " 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 21 (dBASE III) <br /><br /> 277 (dBASE IV) <br /><br /> 533 (dBASE 5.0) |  
|FIL|文件类型 dBase III，dBase IV，或 dBase 5|  
|PAGETIMEOUT|指定页 (如果未使用，则为) 在删除之前保留在缓冲区中的时间段（以十分之一为间隔）。 默认值为 600 (60 秒) 的十分之几秒。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这会设置与 "设置" 对话框中 **页面超时** 相同的选项。|  
|READONLY|若要使文件为只读，则为 TRUE;如果设置为 FALSE，则使文件不为只读。<br /><br /> 这会在 "设置" 对话框中设置与 " **只读** " 相同的选项。|  
|STATISTICS|对于 dBASE 驱动程序，确定表大小统计信息是否近似。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这会设置与 "设置" 对话框中的 " **近似行计数** " 相同的选项。|  
|线程|引擎要使用的后台线程数。 此值为3，无法更改。<br /><br /> 这会设置与 "设置" 对话框中的 **线程** 相同的选项。|
