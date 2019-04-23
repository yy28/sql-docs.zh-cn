---
title: 服务器属性（“执行”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e2d871426345627f88992d4941068681b82cdf0
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59962133"
---
# <a name="server-properties-execution-page"></a>服务器属性（“执行”页）
  使用此页可设置报表执行的超时值。 此值将应用于当前报表服务器实例处理的所有报表。 您可以针对单个报表覆盖此值。 您指定的值必须适合报表服务器上发生的所有报表处理，并适合在报表服务器检索报表中所使用的数据时针对数据库服务器执行的查询处理。  
  
 若要打开此页，请启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器实例，右键单击报表服务器名称，然后选择“属性”。 单击 **“执行”** 将此页打开。  
  
## <a name="options"></a>选项  
 **不对报表执行时间设置超时**  
 允许报表服务器在不受限制的时间内完成报表处理。  
  
 **将报表执行时间限制为(以秒计)**  
 针对报表执行设置时间约束。 在请求报表时将对该时间段开始计时。 如果在报表处理全部完成之前该时间段就已结束，那么报表服务器将取消该处理和所有对外部数据源的处理中的查询。  
  
## <a name="see-also"></a>请参阅  
 [设置报表服务器属性 (Management Studio)](set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](connect-to-a-report-server-in-management-studio.md)   
 [设置报表处理属性](../report-server/set-report-processing-properties.md)   
 [为报表和共享数据集处理设置超时值 (SSRS)](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Management Studio 中报表服务器的 F1 帮助](report-server-in-management-studio-f1-help.md)  
  
  
