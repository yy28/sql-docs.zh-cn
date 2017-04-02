---
title: "使用 Reporting Services 中的 KPI | Microsoft Docs"
ms.date: "02/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# 使用 Reporting Services 中的 KPI
关键绩效指标 (KPI) 是一个视觉提示，用于传达某个目标的进度量。  关键绩效指标对于团队、经理和企业很有价值，可快速评估针对可度量的目标所进行的工作进度。   
  
通过使用 SQL Server 2016 Reporting Services 中的 KPI，你可以轻松地将以下问题的答案可视化：  
  
-   我是超前还是落后？  
  
-   我超前或落后多少？  
  
-   我最少已经完成了多少？  
  
## 创建数据集  
KPI 将只使用共享数据集的第一行数据。 请确保你想要使用的数据位于第一行上。 若要创建共享数据集，可以使用报表生成器或 SQL Server Data Tools。  
  
> **注意**：该 KPI 的数据集不必位于相同文件夹中。  
  
## KPI 的位置  
  
可以在报表服务器中的任何文件夹中创建 KPI。  创建 KPI 前，需要考虑 KPI 的正确放置位置。 建议将它放在用户可见、同时可与周围其他报表和 KPI 相关的文件夹中。  
  
## 添加 KPI  
  
在确定 KPI 的位置之后，转到该文件夹并从顶部菜单中选择“新建” > “KPI”。  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
这将为你显示“新建 KPI”  屏幕。  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
你可以分配静态值，或使用共享数据集的数据。 在创建新的 KPI 时，它将使用一组随机的人工输入数据填充它们。  
  
|字段|Description|  
|---|---|  
|值格式|  用于更改要显示的值的格式。|   
|“值”|要显示的 KPI 的值。|  
|目的|用作数值比较并显示为一个百分比差值。|  
|状态|用于确定 KPI 磁贴颜色的数值。 有效值为 1（绿色）、0（琥珀色）和 -1（红色）。|  
|趋势集|用于图表可视化的逗号分隔的数值。 也可以将其设置为具有表示走向的值的数据集列。|  
  
> **警告**：虽然可以在设计时使用用于“状态”  字段的单词，如果要刷新数据集，还是应当使用数值。 如果使用单词刷新数据集，而不是使用数值，则可能会损坏服务器上的 KPI。  
  
> **请注意**：“值” 、“目标”  和“状态”  字段只能从数据集结果的第一行选择一个值。 但是，“趋势集”  字段中，可以选择反映这种趋势的具体列。  
  
若要使用来自共享数据集的数据，则可以执行以下操作。  
  
1.  将字段下拉框从“手动设置” ，或“未设置” ，更改为“数据集字段” 。  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2.  在数据框中选择 **省略号 (…)** 。 此时会弹出“选择数据集”  屏幕。  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3.  选择包含要显示的数据的数据集。  
  
4.  选择想要使用的字段。 选择“确定”。  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5.  更改“值格式”  以匹配你的值的格式。 在此示例中，值是一种货币。  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6.  选择“应用” 。  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)  
  
## 删除 KPI  
  
若要删除 KPI，可以执行以下操作。  
  
1.  选择想要删除的 KPI 的 **省略号 (…)** 。 选择“管理” 。  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  选择“删除” 。 在确认对话框中再次选择“删除”  。  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## 刷新 KPI  
  
若要刷新 KPI，则需要为共享数据集配置 **缓存刷新计划** 。 目前，你不能在 Web 门户网站配置缓存刷新计划。 建议转到旧报表管理器执行此操作。   
  
这将演示如何设置缓存刷新计划的一些基本设置。 有关缓存刷新计划的详细信息，请参阅 [缓存刷新选项（报表管理器）](Cache%20Refresh%20Options%20(Report%20Manager).xml)。  
  
1.  打开报表管理器，找到你要为其配置缓存刷新计划属性的共享数据集。   
  
2.  悬停在该报表或共享数据集之上，然后选择下拉箭头。  
  
3.  在下拉列表中，选择“管理” 。 将打开“常规属性”  页。  
  
4.  单击“缓存刷新选项”  选项卡。  
  
5.  若要创建新的缓存计划，请选择“新建缓存刷新计划” 。  
  
    ![rsRefreshKPI1](../reporting-services/media/rsrefreshkpi1.png)  
  
6.  你将收到一条消息，询问你是否为此项目以默认选项启用缓存。 选择“确定” 。  
  
    > **注意**：必须启用并启动 SQL Server 代理服务，才能创建缓存刷新计划。  
  
7.  可以选择特定的计划，或选择共享的计划（如果有）。  
  
8.  缓存刷新计划的计划运行时，KPI 的值将更新。  
  
    ![rsRefreshKPI2](../reporting-services/media/rsrefreshkpi2.png)  
  
## 另请参阅  
  
- [Web 门户（SSRS 本机模式）](../reporting-services/web-portal-ssrs-native-mode.md)  
  
- [缓存刷新选项（报表管理器）](Cache%20Refresh%20Options%20(Report%20Manager).xml)  
  
    
  
  
  
