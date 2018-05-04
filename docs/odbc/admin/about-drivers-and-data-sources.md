---
title: 有关驱动程序和数据源 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15b6a801fe6c768df9b0eb92a3faf917ac5a0b86
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="about-drivers-and-data-sources"></a>有关驱动程序和数据源
*驱动程序*是处理 ODBC 请求并将数据返回到应用程序的组件。 如有必要，驱动程序将修改到理解数据源的窗体的应用程序的请求。 必须使用驱动程序的安装程序以添加或删除驱动程序从你的计算机。  
  
 *数据源*是数据库或访问由驱动程序的文件和由数据源名称 (DSN) 标识。 使用 ODBC 数据源管理器来添加、 配置和从系统中删除数据源。 以下表所述的可用的数据源的类型。  
  
|数据源|Description|  
|-----------------|-----------------|  
|用户|用户 Dsn 计算机本地的并可以仅由当前用户。 它们在 HKEY_CURRENT_USER 注册表子树中注册。|  
|系统|系统 Dsn 是计算机的本地而不是专用于用户。 系统或具有权限的用户可以使用数据源使用的系统 DSN 设置。 在 HKEY_LOCAL_MACHINE 注册表子树中注册系统 Dsn。|  
|文件|文件 Dsn 是可以在具有相同的驱动程序安装的所有用户之间共享，因此对数据库的访问的基于文件的源。 这些数据源不需要专用于用户，也不是本地的计算机。 文件数据源名称不会标识由专用的注册表条目;相反，它们是由文件名称标识.dsn 扩展名。|  
  
 用户和系统数据源统称为*机*数据源，因为它们是计算机的本地。  
  
 每个这些数据源有一个选项卡**ODBC 数据源管理器**对话框。 有关数据源的详细信息，请参阅[数据源](../../odbc/reference/data-sources.md)。
