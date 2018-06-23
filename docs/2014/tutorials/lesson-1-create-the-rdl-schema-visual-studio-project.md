---
title: 第 1 课： 创建 RDL 架构 Visual Studio 项目 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f420509c-51aa-4170-8c25-64c2954f4bb9
caps.latest.revision: 17
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: b6c502205f669c48efe1f939ba88e5352205f4de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128451"
---
# <a name="lesson-1-create-the-rdl-schema-visual-studio-project"></a>第 1 课：创建 RDL 架构 Visual Studio 项目
  针对本教程，您将创建一个简单控制台应用程序。 本教程假定你正在开发中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]。  
  
> [!NOTE]  
>  访问在具有高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 上运行的报表服务器 Web 服务时，必须将“_SQLExpress”追加到“ReportServer”路径。 例如：  
>   
>  `http://myserver/reportserver_sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-create-the-web-service-proxy"></a>创建 Web 服务代理  
  
1.  从**启动**菜单上，选择**所有程序**，然后 Microsoft Visual Studio 中，然后**Visual Studio Tools**，，然后**Visual Studio 2010 命令提示**.  
  
2.  在命令提示符窗口中，如果您使用 C#，则运行以下命令：  
  
    ```  
    wsdl /language:CS /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     如果您使用 Visual Basic，则运行以下命令：  
  
    ```  
    wsdl /language:VB /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     此命令将生成一个 .cs 或 .vb 文件。 您将把该文件添加到您的应用程序。  
  
### <a name="to-create-a-console-application"></a>创建控制台应用程序  
  
1.  上**文件**菜单上，指向**新建**，然后单击**项目**以打开**新项目**对话框。  
  
2.  在左窗格中，在**已安装的模板**，单击**Visual Basic**或**Visual C#** 节点，然后选择项目的类别类型从展开的列表。  
  
3.  选择**控制台应用程序**项目类型。  
  
4.  在**名称**框中，输入你的项目的名称。 键入的名称`SampleRDLSchema`。  
  
5.  在**位置**框中，键入你想要保存你的项目，或单击的路径**浏览**以导航到的文件夹。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 您的项目折叠的视图将显示在解决方案资源管理器。  
  
7.  在“项目”菜单上，单击“添加现有项”。  
  
8.  导航到的位置，为.cs 或.vb 文件生成，然后选择该文件，，然后单击**添加**。  
  
     您还需要添加对 <xref:System.Web.Services> 命名空间的引用，Web 引用才能正常工作。  
  
9. 在项目菜单中，单击**添加引用**。  
  
     在**添加引用**对话框中，在 **.NET**选项卡上，选择**System.Web.Services**，然后单击**确定**。  
  
     有关如何连接到报表服务器 Web 服务的详细信息，请参阅[生成应用程序使用 Web 服务和.NET Framework](../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
10. 在解决方案资源管理器中，展开该项目节点。 您将看到默认名称为 Program.cs（对于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，为 Module1.vb）的代码文件已添加到您的项目中。  
  
11. 打开 Program.cs（对于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，为 Module1.vb）文件，并使用以下内容替换该代码：  
  
     以下代码提供了将用于实现加载、更新和保存功能的方法存根 (Stub)。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using ReportService2010;  
  
    namespace SampleRDLSchema  
    {  
        class ReportUpdater  
        {  
            ReportingService2010 _reportService;  
  
            static void Main(string[] args)  
            {  
                ReportUpdater reportUpdater = new ReportUpdater();  
                reportUpdater.UpdateReport();  
            }  
  
            private void UpdateReport()  
            {  
                try  
                {  
                    // Set up the Report Service connection  
                    _reportService = new ReportingService2010();  
                    _reportService.Credentials =  
                        System.Net.CredentialCache.DefaultCredentials;  
                    _reportService.Url =  
                       "http://<Server Name>/reportserver/" +  
                                       "reportservice2010.asmx";  
  
                    // Call the methods to update a report definition  
                    LoadReportDefinition();  
                    UpdateReportDefinition();  
                    PublishReportDefinition();  
                }  
                catch (Exception ex)  
                {  
                    System.Console.WriteLine(ex.Message);  
                }  
            }  
  
            private void LoadReportDefinition()  
            {  
                //Lesson 3: Load a report definition from the report   
                //          catalog  
            }  
  
            private void UpdateReportDefinition()  
            {  
                //Lesson 4: Update the report definition using the    
                //          classes generated from the RDL Schema  
            }  
  
            private void PublishReportDefinition()  
            {  
                //Lesson 5: Publish the updated report definition back   
                //          to the report catalog  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports ReportService2010  
  
    Namespace SampleRDLSchema  
  
        Module ReportUpdater  
  
            Private m_reportService As ReportingService2010  
  
            Public Sub Main(ByVal args As String())  
  
                Try  
                    'Set up the Report Service connection  
                    m_reportService = New ReportingService2010  
                    m_reportService.Credentials = _  
                        System.Net.CredentialCache.DefaultCredentials  
                    m_reportService.Url = _  
                        "http:// <Server Name>/reportserver/" & _  
                               "reportservice2010.asmx"  
  
                    'Call the methods to update a report definition  
                    LoadReportDefinition()  
                    UpdateReportDefinition()  
                    PublishReportDefinition()  
                Catch ex As Exception  
                    System.Console.WriteLine(ex.Message)  
                End Try  
  
            End Sub  
  
            Private Sub LoadReportDefinition()  
                'Lesson 3: Load a report definition from the report   
                '          catalog  
            End Sub  
  
            Private Sub UpdateReportDefinition()  
                'Lesson 4: Update the report definition using the   
                '          classes generated from the RDL Schema  
            End Sub  
  
            Private Sub PublishReportDefinition()  
                'Lesson 5: Publish the updated report definition back   
                '          to the report catalog  
            End Sub  
  
        End Module  
  
    End Namespace   
    ```  
  
## <a name="next-lesson"></a>下一课  
 在下一课中，您将使用 XML 架构定义工具 (Xsd.exe) 从 RDL 架构中生成类，并将其包含在项目中。 请参阅[第 2 课： 从 RDL 架构使用 xsd 工具生成的类](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)。  
  
## <a name="see-also"></a>请参阅  
 [更新报表使用生成的 RDL 架构类&#40;SSRS 教程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  