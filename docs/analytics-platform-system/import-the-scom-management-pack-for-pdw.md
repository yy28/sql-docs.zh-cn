---
title: 导入 SCOM 管理包
description: 请按照以下步骤操作，将 System Center Operations Manager (SCOM) 管理包用于分析平台系统 (AP) 。 从 SCOM 监视并行数据仓库需要管理包。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 770359a9ddb04eb8aaf45af7dd5b95447c30f264
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523864"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>导入 SCOM 管理包分析平台系统
请按照以下步骤操作，将 System Center Operations Manager (SCOM) 管理包用于分析平台系统 (AP) 。 从 SCOM 监视并行数据仓库需要管理包。 
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>开始之前  
**必备条件**  
  
必须安装并运行 System Center Operations Manager 2007 R2。  
  
必须安装管理包。 请参阅 [&#40;Analytics Platform System&#41;安装 SCOM 管理包 ](install-the-scom-management-packs.md)。  
  
## <a name="step-1-import-the-sql-server-appliance-base-management-pack"></a><a name="Step1"></a>步骤1：导入 SQL Server 设备基本管理包  
  
1.  使用 Operations Manager 2007 管理组的 Operations Manager Administrator 角色的成员帐户登录计算机。  
  
2.  在操作控制台中，单击“管理”  。  
  
3.  右键单击“管理包” **** 节点，然后单击“导入管理包” ****。  
  
    ![单击“导入管理包”](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理包列表中，选择要导入的管理包，单击“**选择**”，然后单击“**添加**”。  
  
    ![管理包列表](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜索 " **设备** "，然后向下钻取到 SQL Server 装置基准 "，然后单击" **添加** 两个选项 "。  
  
    ![SQL Server 工具库](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  在选定的底部窗格中有两个管理包后，单击 **"确定"**。  
  
    ![选择两个管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  单击“安装”  。  
  
    ![显示 "选择管理包" 步骤中的 "导入管理包" 向导的屏幕截图，其中安装选项带有红色圆圈。](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成后，单击 " **关闭**"。  
  
    ![完成后，单击“关闭”](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="import-the-monitoring-pack-for-microsoft-sql-server-2008-r2-parallel-data-warehouse-appliance"></a><a name="Step2"></a>导入 Microsoft SQL Server 2008 R2 并行数据仓库设备的监视包  
  
1.  右键单击“管理包” **** 节点，然后单击“导入管理包” ****。  
  
2.  选择 " **从磁盘添加**..."。  
  
    ![右键单击“管理包”](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  请在 "要导入的管理包" 部分中，找到你提取 SQL Server PDW 管理包的位置，然后选择三个管理包。 为此，可以选择第一个，单击 "移动"，然后选择最后一个。 选择所有选项后，单击 " **打开**"。  
  
    ![选择管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  单击“安装”  。  
  
    !["选择管理包" 步骤中的 "导入管理包" 向导的另一屏幕截图，其中安装选项以红色圆圈。](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  单击“关闭”。  
  
    ![单击 "关闭"](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>下一步  
导入管理包后，请继续执行下一步： [配置 SCOM 以监视分析平台系统 &#40;分析平台系统&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
