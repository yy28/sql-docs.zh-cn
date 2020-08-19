---
description: 安装软件 (ODBC)
title: " (ODBC) 安装软件 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], installing
- installing ODBC driver for Oracle [ODBC]
ms.assetid: dfac8ade-eebe-4ebe-a199-feb740ed5bae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe161ef45ef91f67317d7a0b465e00d3d2045c40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449469"
---
# <a name="installing-the-software-odbc"></a>安装软件 (ODBC)
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 用于 Oracle 的 ODBC 驱动程序是数据访问组件之一。 它附带其他 ODBC 组件（如 ODBC 数据源管理器），并且应该已经安装。 还可以在 Microsoft 产品支持服务联机网站上的 "驱动程序和其他下载" 下找到该驱动程序，网址为 [www.microsoft.com](https://www.microsoft.com)。  
  
 网络软件必须根据其自身的文档进行安装。 只要支持网络软件，Oracle 的 ODBC 驱动程序就不需要特殊的安装注意事项。  
  
 Oracle 软件必须按照其自己的文档进行安装。 只要驱动程序支持版本，Oracle 的 ODBC 驱动程序通常不需要特殊的安装注意事项。 但是，为了保持与产品兼容，请安装 Oracle 的 ODBC 驱动程序，以确保具有最新版本的驱动程序。 Oracle 维护一个公共 FTP 站点，其中包含与服务器产品附带的 Oracle 服务器产品和客户端组件的修补程序。 需要这些修补程序才能正常工作多个 Microsoft 产品和技术。 有关此站点的详细信息，请参阅 [Oracle 软件修补程序](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!CAUTION]  
>  通过 MDAC/Windows DAC 安装 Oracle 软件可能会覆盖 MDAC 的当前版本。 如果使用 ODBC 组件时出现问题，请重新安装 MDAC。
