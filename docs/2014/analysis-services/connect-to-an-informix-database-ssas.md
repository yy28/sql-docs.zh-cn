---
title: 连接到 Informix 数据库 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conninformixdb.f1
ms.assetid: b01d537c-1c04-4d7d-9146-051c249b08e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca54a226097860e563fd439261e8ce1f2690cacd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680208"
---
# <a name="connect-to-an-informix-database-ssas"></a>连接到 Informix 数据库 (SSAS)
  **“表导入向导”** 的这一页可用于指定用于连接到 Informix 数据库的设置。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到数据源，必须在计算机上安装适当的访问接口。  
  
> [!NOTE]  
>  在此页中选择数据库时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选数据库中读取，则导入将不会成功。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **友好连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **服务器名称**  
 键入或选择要连接到的服务器实例的名称。  
  
 **用户名**  
 为数据库连接指定用户名。  
  
 在为数据源构造连接字符串时，将使用该用户名。 在“表格属性”窗口和“导入向导”中预览和筛选数据时，也使用这些凭据。 这些凭据不用于导入或刷新数据；而是使用在“模拟信息”页中指定的 Windows 凭据。  
  
 **密码**  
 为数据库连接指定密码。  
  
 **保存我的密码**  
 指定是否存储已在“密码”框中输入的密码。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。 有关详细信息，请参阅[设置高级属性 (SSAS)](set-advanced-properties-ssas.md)。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  
