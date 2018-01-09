---
title: "ADO MD 从迁移到 ADOMD.NET |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, migrating to
- migrating ADO MD to ADOMD.NET
- ADO MD migration [ADOMD.NET]
ms.assetid: 8c760db3-c475-468e-948d-e5f599d985ad
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0c8e51a04bc47537adb9085e11511b73b289e2c5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="migrating-from-ado-md-to-adomdnet"></a>从 ADO MD 迁移到 ADOMD.NET
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]ADOMD.NET 库是类似于 ActiveX 数据对象多维 (ADO MD) 的库中，用来访问基于组件对象模型 (COM） 客户端应用程序中的多维数据 ActiveX 数据对象 (ADO) 库的扩展。 使用 ADO MD 可轻松地通过非托管语言（例如 C++ 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic）访问多维数据。 使用 ADOMD.NET 可轻松地通过托管语言（例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET）访问分析数据（多维数据和数据挖掘数据）。 此外，ADOMD.NET 还提供了增强的元数据对象模型。  
  
 将现有的客户端应用程序从 ADO MD 迁移到 ADOMD.NET 很容易，但其中存在多个有关迁移的重要差异：  
  
 **若要提供对客户端应用程序的连接和数据访问**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|需要对 Adodb.dll 和 Adomd.dll 的引用。|需要对单个 Microsoft.AnalysisServices.AdomdClient.dll 的引用。|  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 类除了可提供对元数据的访问，还可提供连接支持。  
  
 **若要检索的多维对象的元数据**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|使用目录类。|使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> 的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 属性。|  
  
 **若要运行查询并返回单元集对象**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|使用单元集类。|使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 类。|  
  
 **若要访问用于显示单元集的元数据**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|使用位置类。|使用 <xref:Microsoft.AnalysisServices.AdomdClient.Set> 和 <xref:Microsoft.AnalysisServices.AdomdClient.Tuple> 对象。|  
  
> [!NOTE]  
>  支持 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 类以提供向后兼容。  
  
 **若要检索挖掘模型元数据**  
 ADO MD 中有任何类可用。 在 ADOMD.NET 使用数据挖掘集合之一：  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> 包含数据源中所有挖掘模型的列表。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> 提供有关可用挖掘算法的信息。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> 公开有关服务器上的挖掘结构的信息。  
  
 为了突出显示这些差异，下面的迁移示例将现有的 ADO MD 应用程序与等效的 ADOMD.NET 应用程序进行了比较。  
  
## <a name="looking-at-a-migration-example"></a>查看迁移示例  
 本节中显示的现有 ADO MD 和等效的 ADOMD.NET 代码示例执行同一组操作：创建连接、运行多维表达式 (MDX) 语句以及检索元数据和数据。 但是，这两组代码不使用相同的对象来执行上述任务。  
  
### <a name="existing-ado-md-code"></a>现有的 ADO MD 代码  
 下面的代码示例中，从 ADO MD 2.8 文档绘制用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic® 6.0 和使用 ADO MD 来演示如何连接和查询[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据源。 此 ADO MD 示例使用以下对象：  
  
-   从连接创建虚拟机**目录**对象。  
  
-   多维表达式 (MDX) 语句使用运行**单元集**对象。  
  
-   检索元数据和数据从**位置**从检索到的对象**单元集**对象。  
  
```  
Private Sub cmdCellSettoDebugWindow_Click()  
Dim cat As New ADOMD.Catalog  
Dim cst As New ADOMD.Cellset  
Dim i As Integer  
Dim j As Integer  
Dim k As Integer  
Dim strServer As String  
Dim strSource As String  
Dim strColumnHeader As String  
Dim strRowText As String  
  
On Error GoTo Error_cmdCellSettoDebugWindow_Click  
Screen.MousePointer = vbHourglass  
'*-----------------------------------------------------------------------  
'* Set server to local host.  
'*-----------------------------------------------------------------------  
    strServer = "LOCALHOST"  
  
'*-----------------------------------------------------------------------  
'* Set MDX query string source.  
'*-----------------------------------------------------------------------  
    strSource = strSource & "SELECT "  
    strSource = strSource & "{[Measures].members} ON COLUMNS,"  
    strSource = strSource & _  
        "NON EMPTY [Store].[Store City].members ON ROWS"  
    strSource = strSource & " FROM Sales"  
  
'*-----------------------------------------------------------------------  
'* Set active connection.  
'*-----------------------------------------------------------------------  
        cat.ActiveConnection = "Data Source=" & strServer & _  
            ";Provider=msolap;"  
  
'*-----------------------------------------------------------------------  
'* Set cellset source to MDX query string.  
'*-----------------------------------------------------------------------  
        cst.Source = strSource  
  
'*-----------------------------------------------------------------------  
'* Set cellset active connection to current connection  
'*-----------------------------------------------------------------------  
    Set cst.ActiveConnection = cat.ActiveConnection  
  
'*-----------------------------------------------------------------------  
'* Open cellset.  
'*-----------------------------------------------------------------------  
    cst.Open  
  
'*-----------------------------------------------------------------------  
'* Allow space for row header text.  
'*-----------------------------------------------------------------------  
strColumnHeader = vbTab & vbTab & vbTab & vbTab & vbTab & vbTab  
  
'*-----------------------------------------------------------------------  
'* Loop through column headers.  
'*-----------------------------------------------------------------------  
       For i = 0 To cst.Axes(0).Positions.Count - 1  
            strColumnHeader = strColumnHeader & _  
                cst.Axes(0).Positions(i).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
       Next  
       Debug.Print vbTab & strColumnHeader & vbCrLf  
  
'*-----------------------------------------------------------------------  
'* Loop through row headers and provide data for each row.  
'*-----------------------------------------------------------------------  
        strRowText = ""  
        For j = 0 To cst.Axes(1).Positions.Count - 1  
            strRowText = strRowText & _  
                cst.Axes(1).Positions(j).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
            For k = 0 To cst.Axes(0).Positions.Count - 1  
                strRowText = strRowText & cst(k, j).FormattedValue & _  
                    vbTab & vbTab & vbTab & vbTab  
            Next  
            Debug.Print strRowText & vbCrLf  
            strRowText = ""  
        Next  
  
    Screen.MousePointer = vbDefault  
Exit Sub  
  
Error_cmdCellSettoDebugWindow_Click:  
   Beep  
   Screen.MousePointer = vbDefault  
   MsgBox "The following error has occurred:" & vbCrLf & _  
      Err.Description, vbCritical, " Error!"  
   Exit Sub  
End Sub  
```  
  
### <a name="equivalent-adomdnet-code"></a>等效的 ADOMD.NET 代码  
 下面的示例是用 Visual Basic .NET 编写的，并使用 ADOMD.NET 演示了如何执行与早期的 Visual Basic 6.0 示例相同的操作。 下面的示例与前面显示的 ADO MD 示例之间最主要差异是用于执行这些操作的对象。 ADOMD.NET 示例使用下列对象：  
  
-   创建与连接**AdomdConnection**对象。  
  
-   运行 MDX 语句使用**AdomdCommand**对象。  
  
-   检索元数据和数据从**设置**从检索到的对象**单元集**对象。  
  
```  
Private Sub DisplayCellSetInOutputWindow()  
    Dim conn As AdomdConnection  
    Dim cmd As AdomdCommand  
    Dim cst As CellSet  
    Dim i As Integer  
    Dim j As Integer  
    Dim k As Integer  
    Dim strServer As String = "LOCALHOST"  
    Dim strSource As String = "SELECT [Measures].members ON COLUMNS, " & _  
        "NON EMPTY [Store].[Store City].members ON ROWS FROM SALES"  
    Dim strOutput As New System.IO.StringWriter  
  
    '*-----------------------------------------------------------------------  
    '* Open connection.  
    '*-----------------------------------------------------------------------  
    Try  
        ' Create a new AdomdConnection object, providing the connection  
        ' string.  
        conn = New AdomdConnection("Data Source=" & strServer & _  
        ";Provider=msolap;")  
        ' Open the connection.  
        conn.Open()  
    Catch ex As Exception  
        Throw New ApplicationException( _  
            "An error occurred while connecting.")  
    End Try  
  
    Try  
    '*-----------------------------------------------------------------------  
    '* Open cellset.  
    '*-----------------------------------------------------------------------  
        ' Create a new AdomdCommand object, providing the MDX query string.  
        cmd = New AdomdCommand(strSource, conn)  
        ' Run the command and return a CellSet object.  
        cst = cmd.ExecuteCellSet()  
  
    '*-----------------------------------------------------------------------  
    '* Concatenate output.  
    '*-----------------------------------------------------------------------  
  
    ' Include spacing to account for row headers.  
    strOutput.Write(vbTab, 6)  
  
    ' Iterate through the first axis of the CellSet object and  
    ' retrieve column headers.  
    For i = 0 To cst.Axes(0).Set.Tuples.Count - 1  
        strOutput.Write(cst.Axes(0).Set.Tuples(i).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
    Next  
    strOutput.WriteLine()  
  
    ' Iterate through the second axis of the CellSet object and  
    ' retrieve row headers and cell data.  
    For j = 0 To cst.Axes(1).Set.Tuples.Count - 1  
        ' Append the row header.  
        strOutput.Write(cst.Axes(1).Set.Tuples(j).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
  
        ' Append the cell data for that row.  
        For k = 0 To cst.Axes(0).Set.Tuples.Count - 1  
            strOutput.Write(cst.Cells(k, j).FormattedValue)  
            strOutput.Write(vbTab, 4)  
        Next  
        strOutput.WriteLine()  
    Next  
  
    ' Display the output.  
    Debug.WriteLine(strOutput.ToString)  
  
    '*-----------------------------------------------------------------------  
    '* Release resources.  
    '*-----------------------------------------------------------------------  
        conn.Close()  
    Catch ex As Exception  
        ' Ignore or handle errors.  
    Finally  
        cst = Nothing  
        cmd = Nothing  
        conn = Nothing  
    End Try  
End Sub  
```  
  
  
