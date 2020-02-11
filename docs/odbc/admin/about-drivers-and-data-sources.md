---
title: 关于驱动程序和数据源 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e9b7229882b3b7f94e6b059e04c6496bde09641
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938045"
---
# <a name="about-drivers-and-data-sources"></a>关于驱动程序和数据源
*驱动程序*是处理 ODBC 请求并将数据返回到应用程序的组件。 如有必要，驱动程序会将应用程序的请求修改为数据源所理解的形式。 必须使用驱动程序的安装程序在计算机中添加或删除驱动程序。  
  
 *数据源*是由驱动程序访问的数据库或文件，由数据源名称（DSN）标识。 使用 ODBC 数据源管理器可以从系统中添加、配置和删除数据源。 下表介绍了可以使用的数据源类型。  
  
|数据源|说明|  
|-----------------|-----------------|  
|用户|用户 Dsn 是计算机的本地用户，只能由当前用户使用。 它们是在 HKEY_CURRENT_USER 注册表子树中注册的。|  
|系统|系统 Dsn 是计算机的本地系统，而不是专用于用户。 系统或具有权限的任何用户都可以使用使用系统 DSN 设置的数据源。 系统 Dsn 注册在 HKEY_LOCAL_MACHINE 注册表子树中。|  
|文件|文件 Dsn 是基于文件的源，可以在安装了相同驱动程序并因此具有对数据库的访问权限的所有用户之间共享。 这些数据源不需要专用于用户，也不需要是计算机的本地数据源。 专用注册表项不标识文件数据源名称;相反，它们由带有 .dsn 扩展名的文件名标识。|  
  
 由于用户和系统数据源是计算机的*本地数据源*，因此它们统称为计算机数据源。  
  
 其中每个数据源在 " **ODBC 数据源管理器**" 对话框中都有一个选项卡。 有关数据源的详细信息，请参阅 [数据源](../../odbc/reference/data-sources.md)。
