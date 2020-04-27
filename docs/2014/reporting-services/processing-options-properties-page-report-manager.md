---
title: "\"处理选项\" 属性页（报表管理器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 28f07c70-7132-4d15-9505-4fdf31dc9cc0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f91cd8a93571b62f57933ff7556004f8c7b42a9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108035"
---
# <a name="processing-options-properties-page-report-manager"></a>“处理选项”属性页（报表管理器）
  使用“处理选项”属性页可为当前所选的报表设置报表执行属性。 这些选项将确定处理报表数据的时间。 您可以设置这些选项，使报表数据的检索时间错开高峰期。 如果有经常访问的报表，则可以临时缓存其副本，这样，在每隔几分钟便有多个用户访问同一报表的情况下可使用户无需等待。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供报表历史记录、执行快照和缓存功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-processing-options-properties-page"></a>打开“处理选项”属性页  
  
1.  打开报表管理器，找到要设置处理属性的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该报表的“常规”属性页。  
  
4.  选择 **“处理选项”** 选项卡。  
  
## <a name="options"></a>选项  
 **始终用最新数据运行此报表**  
 如果您希望在用户选择报表时检索报表数据，请使用此选项。 如果有缓存的报表副本可用，则会将缓存副本返回给用户；否则，在用户选择报表时将执行数据检索和呈现。  
  
 若要始终以最新数据运行报表，请选择 **“不缓存此报表的临时副本”** 。 每当用户打开报表时，都会触发一个对数据源的查询，该数据源包含报表中所使用的数据。  
  
 若要始终以最新数据运行报表，请选择 ****，则用户首次打开报表时将在缓存中保留报表的临时副本。 以后在缓存期间内运行报表的用户将收到报表的缓存副本。 由于将从缓存中返回报表（而不是重新处理），因此进行缓存通常会改进性能。  
  
 缓存的报表最终必须过期。 请指定要保存报表缓存副本的分钟数。 临时副本一过期，就不会再从缓存中返回该副本。 下次用户打开该报表时，报表服务器将重新处理该报表，并重新将刷新后的报表副本存入缓存。  
  
 您也可以使用计划按一定的频率（而不是具体的分钟数）来设定缓存报表的过期时间。 例如，要使缓存的报表在工作日结束时过期，则可以选择夜间的某个特定时间，该时间过后缓存的报表即过期。  
  
 **根据报表执行快照呈现此报表**  
 使用此选项可检索已在预定时间存储为快照的报表。 选择此选项时，可以将数据处理安排在非高峰期进行。 与用户打开报表时创建的缓存副本不同，快照按计划进行创建和刷新。 快照不会过期并持续有效，直到新版本的快照取而代之。  
  
 由于报表执行设置而生成的快照与报表历史快照具有相同的特点。 不同之处在于仅有一个报表执行快照，而通常可能会有许多报表历史快照。 报表历史快照可以从报表的“历史记录”页进行访问，其中存储了多个存在于不同时间点的报表实例。 相反，用户若要访问报表执行快照，就需按照与访问实时报表相同的方法从文件夹进行访问。 对于报表执行快照，没有可视的信息提示用户该报表为快照。  
  
 选择相关选项 **“在此页上单击‘应用’按钮后创建报表快照”** ，以便在单击“应用”后创建报表快照。 这将立即生成报表快照，以便在计划的开始时间之前提供该报表。  
  
 **报表执行超时**  
 指定在给定的秒数之后报表处理是否超时。 如果选择默认设置，则会将“站点设置”页中指定的超时设置用于此报表。  
  
 此值应用于报表服务器上的报表处理。 它不会设置向报表提供数据的数据库服务器上的数据处理超时值。 但是，所指定的值必须足以完成数据处理和报表处理。 报表处理的计时从选中报表时开始，到打开报表时结束。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表处理属性](report-server/set-report-processing-properties.md)   
 [缓存报表 (SSRS)](report-server/caching-reports-ssrs.md)   
 [创建、修改和删除计划](subscriptions/create-modify-and-delete-schedules.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
