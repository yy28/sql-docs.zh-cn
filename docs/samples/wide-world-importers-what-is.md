---
title: 宽 World 导入程序的 SQL 的示例数据库 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5a1eef0650c520ff4757de627633d096ffa46ec8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33032644"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Wide World Importers 示例数据库的 Microsoft SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
这是虚构的公司 Wide World importers 计划和 SQL Server 和 Azure SQL 数据库进行寻址 WideWorldImporters 示例数据库中的工作流的概述。  

Wide World Importers (WWI) 是批发新奇货物导入程序和从旧金山托架区域运行的分发服务器。

批发商 WWI 的客户将将主要转售的个人的公司。 WWI 销售给零售客户美国各州包括 specialty 存储区，超市，计算存储区、 风景引力商店和某些个人。 WWI 还将销售给其他 wholesalers 通过促销 WWI 的代表的代理的网络。 虽然 WWI 的客户的所有当前基于在美国，公司想要将为扩展推送到其他国家/地区。

WWI 从包括新奇无实用价值制造商和其他新奇 wholesalers 的供应商那里购买商品。 根据需要以执行客户订单，它们常用货物在其 WWI 仓库和从供应商的重新排序。 它们还购买打包材料，大容量和客户的销售这些在较小数量为方便起见。

最近 WWI 开始销售各种如 chilli edible novelties 巧克力。  公司以前不一定非要处理 chilled 的项。 现在，为了满足食品处理要求，它们必须监视其冷却器聊天室和任何具有冷却器部分其卡车中的温度。

## <a name="workflow-for-warehouse-stock-items"></a>仓库常用项的工作流

有关项的库存和分发了典型的流程如下所示：
- WWI 创建采购订单并在提交到供应商订单。
- 供应商发送的项，WWI 接收它们，并在其仓库 stocks 它们。
- 客户从 WWI 排列项
- WWI 填充客户订单与数据仓库中中的常用项，并当它们不具有足够的库存，他们另外订购其他 stock 从供应商。
- 某些客户不希望等待不库存量的项目。 如果他们另外订购了假设五个不同常用项和四个的可用，他们想要接收的四个项目和延期交货剩下的项目。 项将它们发送更高版本中单独装运。
- WWI 发票的常用的项，客户通常通过将顺序转换为发票。
- 客户可能不是库存量的项进行排序。 这些项是延期交货。
- WWI 通过自己传递 van 可，或通过其他快递或运费方法的客户提供常用的项。
- 客户向 WWI 支付发票。
- 我们会定期 WWI 支付供应商的采购订单上的项。 这是通常一段时间后他们收到了商品。

## <a name="data-warehouse-and-analysis-workflow"></a>数据仓库和分析工作流

虽然 WWI 的团队使用 SQL Server Reporting Services 来生成操作报表从 WideWorldImporters 数据库，它们还需要对其数据执行分析并需要生成战略报告。 团队已 WideWorldImportersDW 的数据库中创建的维度的数据模型。 此数据库由 Integration Services 包填充。

SQL Server Analysis Services 用于创建从维空间数据模型中的数据的分析数据模型。 SQL Server Reporting Services 用于直接从维度的数据模型中，以及从分析的模型生成战略报告。 Power BI 用于从相同的数据创建仪表板。 仪表板用于在网站，并在手机和平板电脑上。 *注意： 这些数据模型和报表尚不可用*

## <a name="additional-workflows"></a>其他工作流

这些是其他工作流。
- WWI 问题信用额度说明时由于某种原因，或者当货物发生故障时，客户不会收到良好。 这些被视为负发票。
- WWI 定期对常用的项，以确保他们的系统上显示为可用的常用数量正确无误的有关现有数量进行计数。 （执行此操作的过程称为 stocktake）。
- 冷的房间温度。 易货物存储在 refrigerated 聊天室。 从这些聊天室的传感器数据引入到监视和分析目的的数据库。
- 车辆跟踪位置。 为 WWI 传输商品的汽车包括跟踪的位置的传感器。 此位置重新引入到监视，并进一步分析的数据库。

## <a name="fiscal-year"></a>会计年度

公司所经营在 11 月 1 日开始的财务年份。

## <a name="terms-of-use"></a>使用条款

此处所述的示例数据库和示例代码的许可证： [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

示例数据库包括从 data.gov 和自然 EarthData 已加载的公共数据。 使用条款位于以下位置： [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
