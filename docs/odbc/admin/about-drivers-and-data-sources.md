---
title: 有关驱动程序和数据源 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 69516a613cbd9071686067350ced2ce5ca166a27
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776045"
---
# <a name="about-drivers-and-data-sources"></a>关于驱动程序和数据源
*驱动程序*是处理 ODBC 请求并将数据返回到应用程序的组件。 如有必要，驱动程序将修改到理解数据源的窗体应用程序的请求。 必须使用驱动程序的安装程序以添加或删除驱动程序从您的计算机。  
  
 *数据源*是数据库或访问的驱动程序文件，并由数据源名称 (DSN) 标识。 使用 ODBC 数据源管理器添加、 配置和从系统中删除数据源。 下表所述的可用数据源的类型。  
  
|数据源|Description|  
|-----------------|-----------------|  
|用户|用户 Dsn 计算机本地，并可以仅由当前用户。 它们是在 HKEY_CURRENT_USER 注册表子树中进行注册。|  
|系统|系统 Dsn 是本地的计算机而不是专用于用户。 系统或具有权限的用户可以使用数据源使用的系统 DSN 设置。 在 HKEY_LOCAL_MACHINE 注册表子树中注册系统 Dsn。|  
|文件|文件 Dsn 是基于文件的源，可以在安装了相同驱动程序的所有用户之间共享，因此对数据库的访问。 这些数据源不需要专用于用户，也不是在本地计算机。 文件数据源名称不识别的专用的注册表项;相反，它们通过名称进行标识文件扩展名为.dsn。|  
  
 用户和系统数据源统称为*机*数据源，因为它们是计算机的本地。  
  
 每个这些数据源有一个选项卡**ODBC 数据源管理器**对话框。 有关数据源的详细信息，请参阅 [数据源](../../odbc/reference/data-sources.md)。
