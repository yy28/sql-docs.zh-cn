---
title: "数据配置文件查看器 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 8f02bbe73421c1fbb1f929cef397cfebf749c0d8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="data-profile-viewer"></a>数据配置文件查看器 (Data Profile Viewer)
  数据事件探查过程的下一步是查看和分析数据配置文件。 可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包内运行数据事件探查任务并计算数据配置文件之后，查看这些配置文件。 有关如何设置和运行数据事件探查任务的详细信息，请参阅 [设置数据事件探查任务](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。  
  
> [!IMPORTANT]  
>  输出文件可能包含有关数据库的敏感数据和数据库所包含的数据。 有关如何使此文件更加安全的建议，请参阅 [访问包使用的文件](../../integration-services/security/security-overview-integration-services.md#files)。  
  
## <a name="data-profiles"></a>数据事件探查  
 若要查看数据配置文件，请将数据事件探查任务配置为将其输出发送到文件，然后使用独立的数据配置文件查看器。 若要打开数据配置文件查看器，请执行以下操作之一。  
  
-   在“[!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器”中右键单击“数据事件探查”任务，然后单击“编辑”。 在 **“数据事件探查任务编辑器”** 的 **“常规”** 页上，单击 **“打开配置文件查看器”**。  
  
-   在文件夹中， *\<驱动器 >*: \Program Files (x86) |计划 Files\Microsoft SQL server\110\dts\binn 中，运行 DataProfileViewer.exe。  
  
 该查看器使用多个窗格来显示请求的配置文件和计算所得的结果，包含可选详细信息和明细功能：  
  
 “配置文件”窗格  
 “配置文件”窗格显示数据配置文件任务中所请求的配置文件。 若要查看配置文件的计算结果，请在 **“配置文件”** 窗格中选择配置文件，结果将显示在查看器的其他窗格中。  
  
 **“结果”** 窗格  
 “结果”窗格使用单行来汇总配置文件的计算结果。 例如，如果请求 **“列长度分布配置文件”**，此行将包括最小和最大长度以及行数。 对于大多数配置文件，可以在 **“结果”** 窗格中选择此行，以便在可选的 **“详细信息”** 窗格中查看其他详细信息。  
  
 “详细信息”窗格  
 对于大多数配置文件类型，“详细信息”窗格显示有关在“结果”窗格中选择的配置文件结果的其他信息。 例如，如果请求 **“列长度分布配置文件”**， **“详细信息”** 窗格将显示找到的每列长度。 该窗格还显示列值为该列长度的行数和行数百分比。  
  
 对于对多列进行计算的三种配置文件类型（候选键、函数依赖关系和值包含），“详细信息”窗格显示违反期望关系的信息。 例如，如果请求候选键配置文件，“详细信息”窗格将显示违反候选键唯一性约束的重复值。  
  
 如果有用于计算配置文件的数据源，则可以双击“详细信息”窗格中的行，在“明细”窗格中查看匹配的数据行。  
  
 “明细”窗格  
 在满足以下条件的情况下，可以双击“详细信息”窗格中的行，在“明细”窗格中查看匹配的数据行：  
  
-   有用于计算配置文件的数据源。  
  
-   您有权查看数据。  
  
 为了连接到明细请求的源数据库，数据配置文件查看器使用 Windows 身份验证和当前用户的凭据。 数据配置文件查看器不会使用运行数据事件探查任务的包中存储的连接信息。  
  
> [!IMPORTANT]  
>  数据配置文件查看器中提供的明细功能会将实时查询发送到原始数据源。 这些查询可能会对服务器的性能产生负面影响。  
>   
>  如果从并非最近创建的输出文件中深化，则明细查询所返回的行集可能会与计算原始输出时所使用的行集不同。  
  
 有关数据配置文件查看器的用户界面的详细信息，请参阅 [Data Profile Viewer F1 Help](../../integration-services/control-flow/data-profile-viewer-f1-help.md)。  
  
  
