---
title: 管理签出 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], checkouts
- checkouts [SQL Server Management Studio]
- checking out files
ms.assetid: ddd4adba-d432-4005-9cb2-bb9ee3163d8e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9de9a1f8ceca0fbb05ab2b6680c5fcc34c951109
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183778"
---
# <a name="manage-checkouts"></a>管理签出
  在将文件添加到源代码管理后，您必须签出该文件才能对其进行修改。 将文件签出源代码管理时，源代码管理提供程序会在本地磁盘中创建最新版本的副本并删除该文件的只读属性。 在某些情况下，您可能需要在不签出文件的情况下编辑该文件。 有关编辑文件，而无需签出文件的详细信息，请参阅[编辑 Checked-In 文件](../../2014/database-engine/edit-checked-in-files.md)。  
  
 可以使用[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]手动或自动签出文件。 您手动签出文件通过打开包含中的文件的解决方案[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]环境中，，然后单击**签出**命令。 如果将 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 环境配置为自动签出文件，则可以自动签出文件。  
  
 根据管理员在源代码管理提供程序中设置的选项，还可以使用独占模式或共享模式签出文件。 当您以独占模式签出文件时，只有您能修改文件，在您将文件签入之前，其他任何用户都不能签出该文件。 当您以共享模式签出文件时，任何用户都可以签出同一文件。 每个用户签入文件时，源代码管理提供程序都会尝试将该文件与文件的最新服务器版本进行合并。 如果在签入版本和最新版本之间存在冲突，源代码管理提供程序会提示用户解决这些冲突。  
  
 下表对本部分的主题进行了说明：  
  
|主题|Description|  
|-----------|-----------------|  
|[签出文件](../../2014/database-engine/check-out-files.md)|提供了有关如何签出文件以便进行修改的说明。|  
|[撤消签出](../../2014/database-engine/undo-checkouts.md)|介绍如何取消现有的签出。|  
|[在编辑时自动签出文件](../../2014/database-engine/automatically-check-out-files-upon-edit.md)|介绍如何配置源代码管理，以便在开始编辑文件时将其签出。|  
  
## <a name="see-also"></a>请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [编辑签入文件](../../2014/database-engine/edit-checked-in-files.md)  
  
  
