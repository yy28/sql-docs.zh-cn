---
title: 第 3 课： 从报表服务器加载报表定义 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ad8b31c-43b0-4481-a31b-090cbed4a438
caps.latest.revision: 16
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 912a149542133a4c2bbdf4dfecde2ac0313defd5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024463"
---
# <a name="lesson-3-load-a-report-definition-from-the-report-server"></a>第 3 课：从报表服务器加载报表定义
  创建项目并从 RDL 架构生成类之后，您就可以从报表服务器加载报表定义了。  
  
### <a name="to-load-a-report-definition"></a>加载报表定义  
  
1.  在顶部添加一个私有字段`ReportUpdater`类 (如果你使用的模块[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 为`Report`类。 此字段将用于在应用程序的生存期内维护对从报表服务器加载的报表的引用。  
  
    ```csharp  
    private Report _report;  
    ```  
  
    ```vb  
    Private m_report As Report  
    ```  
  
2.  用以下代码替换 Program.cs 文件（对于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，为 Module1.vb）中 `LoadReportDefinition()` 方法的代码：  
  
    ```csharp  
    private void LoadReportDefinition()  
    {  
        System.Console.WriteLine("Loading Report Definition");  
  
        string reportPath =   
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012";  
  
        // Retrieve the report defintion   
        // from the report server  
        byte[] bytes =   
            _reportService.GetItemDefinition(reportPath);  
  
        if (bytes != null)  
        {  
            XmlSerializer serializer =   
                new XmlSerializer(typeof(Report));  
  
            // Load the report bytes into a memory stream  
            using (MemoryStream stream = new MemoryStream(bytes))  
            {  
                // Deserialize the report stream to an   
                // instance of the Report class  
                _report = (Report)serializer.Deserialize(stream);  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub LoadReportDefinition()  
  
        System.Console.WriteLine("Loading Report Definition")  
  
        Dim reportPath As String = _  
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012"  
  
        'Retrieve the report defintion   
        'from the report server  
        Dim bytes As Byte() = _  
            m_reportService.GetItemDefinition(reportPath)  
  
        If Not (bytes Is Nothing) Then  
  
            Dim serializer As XmlSerializer = _  
                New XmlSerializer(GetType(Report))  
  
            'Load the report bytes into a memory stream  
            Using stream As MemoryStream = New MemoryStream(bytes)  
  
                'Deserialize the report stream to an   
                'instance of the Report class  
                m_report = CType(serializer.Deserialize(stream), _  
                                 Report)  
  
            End Using  
  
        End If  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>下一课  
 在下一课中，您将学习如何编写用于更新从报表服务器加载的报表定义的代码。 请参阅[第 4 课： 以编程方式更新报表定义](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [更新报表使用生成的 RDL 架构类&#40;SSRS 教程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  