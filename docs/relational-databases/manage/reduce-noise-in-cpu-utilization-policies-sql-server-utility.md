---
title: 减少 CPU 使用策略中的干扰（SQL Server 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9fc6db57277044267a89cc89e6c196c782ea920
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115352"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>减少 CPU 使用策略中的干扰（SQL Server 实用工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用以下策略可以减少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具资源使用策略中报告的干扰和意外的策略违反情况。  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>违反处理器使用率策略的频度有多高后才应报告为使用过度？  
 评估时间段和违反百分比公差均可使用实用工具资源管理器的 **“实用工具管理”** 节点中的 **“策略”** 选项卡设置进行配置。 若要更改策略，请使用策略说明右侧的滑块控件，然后单击 **“应用”** 。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   数据收集间隔为 15 分钟。 此值是不可配置的。  
  
-   处理器使用策略的默认阈值上限是 70%。 选项范围是从 0% 到 100%。  
  
-   处理器使用过度的默认评估期是 1 小时。 选项范围是从 1 小时到 1 周。  
  
-   在达到该值之后会将 CPU 报告为利用使用的违反策略的数据点的默认百分比是 20%。 选项范围是从 0% 到 100%。  
  
 例如，基于默认值，每小时将收集 4 个数据点，并且策略阈值为 20%。 因此，默认情况下，1 小时收集期中的任何策略违反都将是 4 个数据点的 25%。 这些默认值将报告任何违反 CPU 使用过度策略阈值的情况。  
  
 若要减少单个策略违反情况产生的干扰，请考虑以下选项：  
  
-   以 1 小时为增量将评估期增加到 6 小时。 6 小时中的单个策略违反情况将是示例大小 24 中的 1 个数据点。 在此情况下，该策略将容忍在 6 小时中有 4 个策略阈值违反情况（16.7% 的数据点），但如果在 6 小时的收集期中有 5 个或更多的策略违反情况（>20% 的数据点），则会报告使用过度。  
  
-   以 1 为增量将违反策略百分比的公差增加到 30%。 1 小时中的单个策略违反情况将是示例大小 4 中的 1 个数据点。 在此情况下，该策略容忍每小时 1 个策略违反，但如果在 1 小时的收集期中有 2 个或更多的策略违反（>30% 的数据点），则会报告使用过度。  
  
-   增加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 托管实例和数据层应用程序的处理器使用率的策略阈值。 有关如何为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例或数据层应用程序更改全局 CPU 使用策略的详细信息，请参阅 [实用工具管理（SQL Server 实用工具）](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)。 有关如何为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的单独实例更改 CPU 使用策略的详细信息，请参阅[托管实例详细信息（SQL Server 实用工具）](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)。 有关如何为单独的数据层应用程序更改 CPU 使用策略的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>违反处理器使用率策略的频度有多高后才应报告为使用不足？  
 评估时间段和违反百分比公差均可使用实用工具资源管理器的 **“实用工具管理”** 节点中的 **“策略”** 选项卡设置进行配置。 若要更改策略，请使用策略说明右侧的滑块控件，然后单击 **“应用”** 。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   数据收集间隔为 15 分钟。 此值是不可配置的。  
  
-   处理器使用策略的默认阈值下限是 0%。 选项范围是从 0% 到 100%。  
  
-   处理器使用不足的默认评估期是 1 周。 选项范围是从 1 天到 1 个月。  
  
-   在达到该值之后会将 CPU 报告为使用不足的违反策略的数据点的默认百分比是 90%。 选项范围是从 0% 到 100%。  
  
 基于默认值，每周收集 672 个数据点，但策略阈值是 0%。 因此，默认情况下，该策略不会生成处理器使用不足违反策略情况。 有关如何为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例或数据层应用程序更改全局 CPU 使用策略的详细信息，请参阅 [实用工具管理（SQL Server 实用工具）](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)。 有关如何为 SQL Server 的单独实例更改 CPU 使用策略的详细信息，请参阅[托管实例详细信息（SQL Server 实用工具）](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)。 有关如何为单独的数据层应用程序更改 CPU 使用策略的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
## <a name="see-also"></a>另请参阅  
 [实用工具管理（SQL Server 实用工具）](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)   
 [在 SQL Server 实用工具中监视 SQL Server 的实例](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [修改资源运行状况策略定义（SQL Server 实用工具）](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
