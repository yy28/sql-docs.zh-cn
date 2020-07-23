---
title: 连接到 Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- connOra
ms.assetid: 711ac7ff-5d3d-4533-80ca-d1fecdb3048f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9be5e4b3652dec337583123e0232ce9b1442af73
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923978"
---
# <a name="connect-to-oracle"></a>连接到 Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  在您首次添加或编辑在 CDC 实例中使用的表时，系统可能会请求您连接到 Oracle 数据库。 您应该输入可访问要捕获表的架构的 Oracle 用户的凭据。 在此对话框中输入以下信息：  
  
 **身份验证**  
  
 选择以下方案之一：  
  
-   **Windows 身份验证**：选择此选项可使用当前的 Windows 域凭据。 只有当 Oracle 数据库配置为使用 Windows 身份验证时，才可以使用此选项。  
  
-   **Oracle 身份验证**：如果选择此选项，则必须在您连接到的 Oracle 数据库中为用户键入 **“用户名”** 和 **“密码”** 。  
  
## <a name="see-also"></a>另请参阅  
 [将表添加到 CDC 实例](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)  
  
  
