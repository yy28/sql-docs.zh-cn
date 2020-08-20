---
description: 配置组件
title: 配置组件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8a4b0f0b0a7a99409b5bb9caea53f23b62457e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487430"
---
# <a name="configuration-components"></a>配置组件
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 数据源是由安装程序 DLL 配置的，后者反过来会在需要时调用驱动程序安装 dll 和转换器安装 Dll。 安装程序 DLL 可以直接从 "控制面板" 中调用，也可以由其他程序（称为 *管理程序*）加载和调用。 下图显示了配置组件之间的关系。  
  
 ![配置组件之间的关系](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 有关这些组件的详细信息，请参阅本节末尾的以下主题。  
  
-   [安装程序](../../../odbc/reference/install/setup-program.md)  
  
-   [安装程序 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驱动程序安装程序 DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>另请参阅  
 [安装组件](../../../odbc/reference/install/installation-components.md)
