---
title: 指定连接字符串 (SSAS) |Microsoft 文档
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
- sql12.asvs.bidtoolset.speconnstring.f1
ms.assetid: 3f89b55b-2659-4e9f-a3ad-ab9a23b6942d
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fc0988701ba21ef7e6880b85abab6309479a8a2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128190"
---
# <a name="specify-a-connection-string-ssas"></a>指定连接字符串 (SSAS)
  **“表导入向导”** 的这一页可用于指定要连接到 OLE DB 或 ODBC 数据源的连接字符串。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到数据源，必须在计算机上安装适当的访问接口。 有关支持的数据源和提供程序的详细信息，请参阅[支持的数据源（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **此连接的友好名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **连接字符串**  
 键入用于连接到 OLE DB 或 ODBC 数据源的连接字符串。  
  
 **生成**  
 通过使用“数据链接属性”对话框，指定连接字符串的属性。 有关详细信息，请参阅 Microsoft 数据链接帮助，可以从该对话框找到该帮助。  
  
 **测试连接**  
 使用指定的连接字符串尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  