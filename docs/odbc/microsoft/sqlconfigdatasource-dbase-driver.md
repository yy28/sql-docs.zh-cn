---
title: "SQLConfigDataSource (dBASE 驱动程序) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17b90ca3ab230aadaa764b58f3399172686502af
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 驱动程序)
> [!NOTE]  
>  本主题提供 dBASE 特定于驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序的序列。<br /><br /> 序列可以是： ASCII （默认值） 或 International。<br /><br /> 这将设置为相同的选项**排序规则序列**在安装程序对话框中。|  
|DEFAULTDIR|所指定的路径的目录。|  
|DELETED|对于 dBASE 驱动程序，指定可以检索或位于已标记为删除的行。 如果未显示设置为 1，已删除的行;如果设置为 0，已删除的行未被删除的行被同等对待。<br /><br /> 这将设置为相同的选项**显示删除行**在安装程序对话框中。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置为相同的选项**说明**在安装程序对话框中。|  
|DRIVER|到驱动程序 DLL 路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|文件键入 dBase III、 IV，dBase 或 dBase 5|  
|PAGETIMEOUT|以十分之一第二个，页 （如果未使用） 在被删除之前保留在缓冲区中指定的时间，段。 默认值为 600 秒 （60 秒） 的十分之几。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**页超时**在安装程序对话框中。|  
|READONLY|若要使文件成为只读的;如果为 FALSE，以使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**在安装程序对话框中。|  
|STATISTICS|对于 dBASE 驱动程序，确定是否近似表大小统计信息。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**大致行计数**在安装程序对话框中。|  
|线程|要使用的引擎的后台线程数。 此值为 3，不能更改。<br /><br /> 这将设置为相同的选项**线程**在安装程序对话框中。|
