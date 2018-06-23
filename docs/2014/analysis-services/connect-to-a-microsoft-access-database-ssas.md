---
title: 连接到 Microsoft Access 数据库 (SSAS) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.connaccessdb.f1
ms.assetid: 9fa81839-dd8b-41d3-915e-c774a707ed53
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 92a5f0b94e41cf2d5bf72a7bb22417888ca946b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026438"
---
# <a name="connect-to-a-microsoft-access-database-ssas"></a>连接到 Microsoft Access 数据库 (SSAS)
  **“表导入向导”** 的这一页可用于指定用于连接到 Microsoft Access 数据库的设置。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到 Microsoft Access 数据库，必须在计算机上安装适当的 ACE 访问接口。 有关详细信息，请参阅[数据源支持（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
> [!NOTE]  
>  在此页中选择文件时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选文件中读取，则导入将不会成功。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **友好连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **数据库名称**  
 指定 Microsoft Access 数据库文件的完整路径。  
  
 **“浏览”**  
 导航至 Microsoft Access 数据库文件可用的位置。  
  
 **用户名**  
 为数据库连接指定用户名。  
  
 **密码**  
 为数据库连接指定密码。  
  
 **保存我的密码**  
 指定是否存储已在“密码”框中输入的密码。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  