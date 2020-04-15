---
title: 关于驱动程序和数据源 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dffeea3bea7e3fbfa66e534ecaa758fbc2064d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307218"
---
# <a name="about-drivers-and-data-sources"></a>关于驱动程序和数据源
*驱动程序*是处理 ODBC 请求并将数据返回给应用程序的组件。 如有必要，驱动程序将应用程序的请求修改为数据源可以理解的窗体。 您必须使用驱动程序的安装程序从计算机添加或删除驱动程序。  
  
 *数据源*是驱动程序访问的数据库或文件，由数据源名称 （DSN） 标识。 使用 ODBC 数据源管理员从系统中添加、配置和删除数据源。 下表描述了可以使用的数据源类型。  
  
|数据源|描述|  
|-----------------|-----------------|  
|用户|用户 DSN 是计算机的本地，只能由当前用户使用。 它们在HKEY_CURRENT_USER注册表子树中注册。|  
|系统|系统 DSN 是计算机的本地，而不是专用于用户。 系统或任何具有权限的用户可以使用使用系统 DSN 设置的数据源。 系统 DSN 在HKEY_LOCAL_MACHINE注册表子树中注册。|  
|文件|文件 DSN 是基于文件的源，可以在安装了相同驱动程序的所有用户之间共享，因此可以访问数据库。 这些数据源不需要专用于用户，也不需要是计算机的本地数据源。 文件数据源名称不由专用注册表项标识;相反，它们由具有 .dsn 扩展名的文件名标识。|  
  
 用户和系统数据源统称为*计算机*数据源，因为它们是计算机的本地数据源。  
  
 每个数据源在**ODBC 数据源管理员**对话框中都有一个选项卡。 有关数据源的详细信息，请参阅 [数据源](../../odbc/reference/data-sources.md)。
