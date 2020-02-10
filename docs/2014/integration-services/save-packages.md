---
title: 保存包 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e4e9c8ea3300c35cb75d451206ab9869f932814
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62889320"
---
# <a name="save-packages"></a>保存包
  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，通过使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器可以生成包，并将包作为 XML 文件（.dtsx 文件）保存到文件系统中。 还可以将包 XML 文件的副本保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 msdb 数据库，或保存到包存储区。 包存储区表示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理的文件系统位置中的文件夹。  
  
 如果将包保存到文件系统，则稍后可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务将包导入到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或包存储区。 有关详细信息，请参阅[导入和导出包（SSIS 服务）](../../2014/integration-services/import-and-export-packages-ssis-service.md)。  
  
 还可以使用命令提示实用工具 **dtutil** 在文件系统和 msdb 之间复制包。 有关详细信息，请参阅 [dtutil Utility](dtutil-utility.md)。  
  
### <a name="to-save-a-package"></a>保存包  
  
-   [将包保存到文件系统](../../2014/integration-services/save-a-package-to-the-file-system.md)  
  
-   [保存一个包副本](../../2014/integration-services/save-a-copy-of-a-package.md)  
  
  
