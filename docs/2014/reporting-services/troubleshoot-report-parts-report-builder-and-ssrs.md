---
title: 报表部件 （报表生成器和 SSRS） 故障排除 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8d76eb115628cc4b63d9eb37494e3fa45e2f7fc2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013778"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>报表部件故障排除（报表生成器和 SSRS）
  下面的这些技巧可在您使用报表部件时对您有所帮助。  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>为何我的同事和我在搜索报表部件时对于同一个报表部件看到不同的实例？  
 在报表服务器上或者与报表服务器相集成的 SharePoint 站点上，对于单个报表部件可能存在多个实例，并且所有实例将具有相同的全局唯一标识符 (GUID)。 在搜索结果列表中仅显示最新实例。 在某些情况下，单个报表部件的不同实例可能拥有不同的权限。 如果您的同事与您对服务器拥有的权限不同，你们将不会看到同一个实例。 例如，假定全都具有相同 GUID 的报表部件的多个副本保存在 SharePoint 集成模式下报表服务器上的不同文件夹中。 如果这些文件夹具有不同的权限，则它们中的报表部件也将具有不同的权限。  
  
 若要查看您和您的同事拥有哪些权限，请咨询报表服务器管理员。  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>在我搜索已上载到 SharePoint 服务器的报表部件时，我看不到它们。 为什么看不到？  
 如果报表部件是您手动上载到 SharePoint 文档库中的，而非通过使用报表生成器发布的，则这些报表部件在报表部件库中可能不出现。 用于库搜索的报表服务器可能需要与 SharePoint 文档库的内容保持同步。 有关详细信息，请参阅[激活报表服务器文件同步功能在 SharePoint 管理中心内](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][联机丛书](https://go.microsoft.com/fwlink/?LinkId=154888)msdn.microsoft.com 上。  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>为何其他人在其报表中看不到图像？  
 如果您发布的报表部件是指向某一图像文件的链接，则该报表部件实际上只是链接。 如果其他人在将图像报表部件添加到其报表后看不到图像，则他们可能对您链接到的图像不具备权限。  
  
 此种情况有几个可能的解决方案：  
  
-   使该图像文件成为报表部件，而不是使指向图像文件的链接成为报表部件。  
  
-   将图像文件移到其他人具有权限的位置。  
  
-   咨询报表服务器管理员以更改权限。  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>在我尝试发布我的报表部件时，为什么系统显示“循环引用”错误消息？  
 如果报表项具有循环引用，则您无法将其作为报表部件发布。 例如，某一报表项指向一个数据集，而该数据集又指向一个参数。 而该参数又指向该数据集。 您将需要首先删除其中一个引用，然后才能发布该报表部件。  
  
## <a name="see-also"></a>请参阅  
 [报表部件（报表生成器和 SSRS）](report-parts-report-builder-and-ssrs.md)  
  
  
