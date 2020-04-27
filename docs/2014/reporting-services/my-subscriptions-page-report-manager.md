---
title: "\"我的订阅\" 页（报表管理器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 491a85a3-f323-4155-a0a8-de2779899995
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 75d662f677ee2b6bbab8e445804ca7f142b5c034
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108192"
---
# <a name="my-subscriptions-page-report-manager"></a>“我的订阅”页（报表管理器）
  使用“我的订阅”页可以在同一位置查看您的所有订阅。 使用此页可以访问、修改或删除您拥有的任何订阅。 您只拥有您所创建的订阅。 您不能访问其他用户的订阅，也不能访问您可使用但不能拥有的订阅（例如，如果您的名称已添加到由另一个用户定义的某个现有订阅中）。 您不能从本页创建订阅。 有关创建订阅的详细信息，请参阅 "[新建订阅" 或 "编辑订阅" 页 &#40;报表管理器&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md)。  
  
 默认情况下，订阅按报表名的字母顺序排列。 单击不同的列标题可以更改订阅的排序方式。 如果没有任何订阅或者禁用了创建或管理订阅的权限，则该页不显示任何订阅。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-my-subscriptions-page"></a>打开“我的订阅”页  
  
1.  打开报表管理器。  
  
2.  在页面顶部的右角，单击“我的订阅”。  
  
    > [!NOTE]  
    >  “我的订阅”始终可用，即使不具备创建订阅的权限也可使用。  
  
## <a name="options"></a>选项  
 **删除**  
 选中要删除的每个订阅旁边的复选框，再单击 **“删除”**。  
  
 **编辑**  
 单击此选项可查看或编辑说明。  
  
 **报告**  
 显示在订阅中指定的报表。 单击报表名称可以查看该报表。  
  
 **说明**  
 显示订阅的说明。 单击说明可以查看或编辑报表的订阅信息。  
  
 **Folder**  
 显示包含在订阅中指定的报表的文件夹。 单击文件夹名称可以查看该文件夹的内容。  
  
 **触发器**  
 标识导致订阅运行的条件。 **TimedSubscription** 触发器基于定义订阅运行时间的计划。 **SnapshotUpdated** 触发器基于对报表快照的更新操作。  
  
 **上次运行时间**  
 显示上次处理订阅的时间。  
  
 **状态**  
 显示订阅的状态。 通常，状态值为“新建”或订阅上次运行的日期和时间。  
  
 当订阅包括指向不再有效的加密值（即指向用于运行报表的已存储凭据）的指针时，将出现“错误数据”状态值。 在报表服务器上重新创建用于对数据进行加密和解密的对称密钥后，现有的加密值将无法使用。  
  
 如果订阅已停用，将无法对其进行处理。 若要更新订阅并使其可操作，请先打开订阅，然后保存即可。  
  
## <a name="see-also"></a>另请参阅  
 [订阅和传递 (Reporting Services)](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
