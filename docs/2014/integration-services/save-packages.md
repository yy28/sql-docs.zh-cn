---
title: 保存包 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 567efb17fb672be6a82fd0f47b52d8919ea81095
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259403"
---
# <a name="save-packages"></a>保存包
  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，通过使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器可以生成包，并将包作为 XML 文件（.dtsx 文件）保存到文件系统中。 还可以将包 XML 文件的副本保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 msdb 数据库，或保存到包存储区。 包存储区表示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理的文件系统位置中的文件夹。  
  
 如果将包保存到文件系统，则稍后可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务将包导入到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或包存储区。 有关详细信息，请参阅[导入和导出包（SSIS 服务）](../../2014/integration-services/import-and-export-packages-ssis-service.md)。  
  
 还可以使用命令提示实用工具 **dtutil** 在文件系统和 msdb 之间复制包。 有关详细信息，请参阅 [dtutil Utility](dtutil-utility.md)。  
  
### <a name="to-save-a-package"></a>保存包  
  
-   [将包保存到文件系统](../../2014/integration-services/save-a-package-to-the-file-system.md)  
  
-   [保存一个包副本](../../2014/integration-services/save-a-copy-of-a-package.md)  
  
  
