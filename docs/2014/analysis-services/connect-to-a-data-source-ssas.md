---
title: 连接到数据源 (SSAS) |Microsoft 文档
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
- sql12.asvs.bidtoolset.conndatasource.f1
ms.assetid: 1e2b17e9-092b-4af1-8a58-c52b8fe10ff1
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f33af08d91f2c8e739c9295daed0ae47563ede51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025831"
---
# <a name="connect-to-a-data-source-ssas"></a>连接到数据源 (SSAS)
  **“表导入向导”** 的这一页可用于创建与各种数据源（例如关系数据库、数据馈送和文件）的新数据源连接。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到数据源，必须在计算机上安装适当的访问接口。 您还必须在工作区数据库服务器上安装有适当的访问接口。 对于 32 位 (x86) 服务器，必须安装 32 位访问接口。 对于 64 位 (x64) 服务器，必须安装 64 位访问接口。  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 始终在 32 位进程，而不考虑体系结构中运行。 在 64 位计算机上运行 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 时，如果安装数据访问接口，您应该知道以下事项：  
  
-   对于支持 32 位和 64 位访问接口的并行安装的访问接口，您应该安装这两个访问接口。  
  
-   对于 ACE 访问接口，您必须安装该访问接口的 64 位版本。 因为 Office 自动安装 ACE 访问接口，所以您不应在承载工作区数据库服务器的 64 位计算机上安装 Microsoft Office 的 32 位版本。  
  
     该 ACE 访问接口用于从文本文件、Excel 文件和 Access 文件导入。 如果不需要对这些数据源的支持，则您可以在运行 64 位工作区数据库服务器的计算机上运行 Microsoft Office 的 32 位版本。  
  
-   对于不支持 32 位和 64 位访问接口的并行安装的其他访问接口，您必须安装 32 位访问接口。 如果只有 64 位计算机可用，则您必须将安装有 64 位访问接口的远程计算机用作工作区数据库服务器。  
  
  