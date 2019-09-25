## How to extract attachments from PDF with PDF extractor SDK in ASP.NET C# using ByteScout Premium Suite

### Step-by-step tutorial on how to extract attachments from PDF with PDF extractor SDK in ASP.NET C#

The sample source codes on this page shows how to extract attachments from PDF with PDF extractor SDK in ASP.NET C#. ByteScout Premium Suite is the set that includes 12 SDK products from ByteScout including tools and components for PDF, barcodes, spreadsheets, screen video recording and you can use it to extract attachments from PDF with PDF extractor SDK with ASP.NET C#.

Want to quickly learn? This fast application programming interfaces of ByteScout Premium Suite for ASP.NET C# plus the guidelines and the code below will help you quickly learn how to extract attachments from PDF with PDF extractor SDK. Follow the instructions from scratch to work and copy the ASP.NET C# code. Use of ByteScout Premium Suite in ASP.NET C# is also described in the documentation included along with the product.

Trial version of ByteScout Premium Suite is available for free. Source code samples are included to help you with your ASP.NET C# app.

## REQUEST FREE TECH SUPPORT

[Click here to get in touch](https://bytescout.zendesk.com/hc/en-us/requests/new?subject=ByteScout%20Premium%20Suite%20Question)

or just send email to [support@bytescout.com](mailto:support@bytescout.com?subject=ByteScout%20Premium%20Suite%20Question) 

## ON-PREMISE OFFLINE SDK 

[Get Your 60 Day Free Trial](https://bytescout.com/download/web-installer?utm_source=github-readme)
[Explore SDK Docs](https://bytescout.com/documentation/index.html?utm_source=github-readme)
[Sign Up For Online Training](https://academy.bytescout.com/)


## ON-DEMAND REST WEB API

[Get your API key](https://pdf.co/documentation/api?utm_source=github-readme)
[Explore Web API Documentation](https://pdf.co/documentation/api?utm_source=github-readme)
[Explore Web API Samples](https://github.com/bytescout/ByteScout-SDK-SourceCode/tree/master/PDF.co%20Web%20API)

## VIDEO REVIEW

[https://www.youtube.com/watch?v=NEwNs2b9YN8](https://www.youtube.com/watch?v=NEwNs2b9YN8)




<!-- code block begin -->

##### ****Default.aspx:**
    
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="ExtractAttachments._Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
    <title>Untitled Page</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
    
    </div>
    </form>
</body>
</html>

```

<!-- code block end -->    

<!-- code block begin -->

##### ****Default.aspx.cs:**
    
```
using System;
using Bytescout.PDFExtractor;

namespace ExtractAttachments
{
    public partial class _Default : System.Web.UI.Page
    {

        /*
        IF YOU SEE TEMPORARY FOLDER ACCESS ERRORS: 

        Temporary folder access is required for web application when you use ByteScout SDK in it.
        If you are getting errors related to the access to temporary folder like "Access to the path 'C:\Windows\TEMP\... is denied" then you need to add permission for this temporary folder to make ByteScout SDK working on that machine and IIS configuration because ByteScout SDK requires access to temp folder to cache some of its data for more efficient work.

        SOLUTION:

        If your IIS Application Pool has "Load User Profile" option enabled the IIS provides access to user's temp folder. Check user's temporary folder

        If you are running Web Application under an impersonated account or IIS_IUSRS group, IIS may redirect all requests into separate temp folder like "c:\temp\".

        In this case
        - check the User or User Group your web application is running under
        - then add permissions for this User or User Group to read and write into that temp folder (c:\temp or c:\windows\temp\ folder)
        - restart your web application and try again

        */

        protected void Page_Load(object sender, EventArgs e)
        {
            String inputFile = Server.MapPath(@".\bin\attachments.pdf");

            // Create Bytescout.PDFExtractor.AttachmentExtractor instance
            AttachmentExtractor extractor = new AttachmentExtractor();
            extractor.RegistrationName = "demo";
            extractor.RegistrationKey = "demo";

            // Load sample PDF document
            extractor.LoadDocumentFromFile(inputFile);

            Response.Clear();
            Response.ContentType = "text/html";

            for (int i = 0; i < extractor.Count; i++)
            {
                string attachmentFileName = extractor.GetFileName(i);
                int attachmentFileSize = extractor.GetSize(i);

                Response.Write("Found attachment: " + attachmentFileName + "<br/>");

                // You can save the attachment to a file
                //extractor.Save(i, attachmentFileName);

                 // ... or write to output stream
                //extractor.Save(i, Response.OutputStream);

                Response.Write("- file size: " + attachmentFileSize + "<br/><br/>");
            }

            Response.End();

            extractor.Dispose();
        }
    }
}

```

<!-- code block end -->    

<!-- code block begin -->

##### ****Default.aspx.designer.cs:**
    
```
//------------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by a tool.
//     Runtime Version:2.0.50727.42
//
//     Changes to this file may cause incorrect behavior and will be lost if
//     the code is regenerated.
// </auto-generated>
//------------------------------------------------------------------------------

namespace ExtractAttachments
{

    public partial class _Default
    {
        protected System.Web.UI.HtmlControls.HtmlForm form1;
    }
}

```

<!-- code block end -->    

<!-- code block begin -->

##### ****ExtractAttachments.csproj:**
    
```
<?xml version="1.0" encoding="utf-8"?>
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="4.0">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" Condition="Exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props')" />
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
    <ProductVersion>9.0.30729</ProductVersion>
    <SchemaVersion>2.0</SchemaVersion>
    <ProjectGuid>{A8705DB2-82C7-46E7-8786-058EEE78DE9D}</ProjectGuid>
    <ProjectTypeGuids>{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}</ProjectTypeGuids>
    <OutputType>Library</OutputType>
    <AppDesignerFolder>Properties</AppDesignerFolder>
    <RootNamespace>ExtractAttachments</RootNamespace>
    <AssemblyName>ExtractAttachments</AssemblyName>
    <FileUpgradeFlags>
    </FileUpgradeFlags>
    <OldToolsVersion>3.5</OldToolsVersion>
    <UpgradeBackupLocation>
    </UpgradeBackupLocation>
    <TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
    <TargetFrameworkProfile />
    <UseIISExpress>false</UseIISExpress>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <Optimize>false</Optimize>
    <OutputPath>bin\</OutputPath>
    <DefineConstants>DEBUG;TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
    <DebugType>pdbonly</DebugType>
    <Optimize>true</Optimize>
    <OutputPath>bin\</OutputPath>
    <DefineConstants>TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
  </PropertyGroup>
  <ItemGroup>
    <Reference Include="Bytescout.PDFExtractor, Version=6.10.0.2136, Culture=neutral, PublicKeyToken=f7dd1bd9d40a50eb, processorArchitecture=MSIL">
      <SpecificVersion>False</SpecificVersion>
      <HintPath>C:\Program Files\Bytescout PDF Extractor SDK\net4.00\Bytescout.PDFExtractor.dll</HintPath>
    </Reference>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Data.DataSetExtensions" />
    <Reference Include="System.Drawing" />
    <Reference Include="System.Web" />
    <Reference Include="System.Web.ApplicationServices" />
    <Reference Include="System.Web.DynamicData" />
    <Reference Include="System.Web.Entity" />
    <Reference Include="System.Web.Extensions" />
    <Reference Include="System.Web.Extensions.Design" />
    <Reference Include="System.Xml" />
    <Reference Include="System.Configuration" />
    <Reference Include="System.Web.Services" />
    <Reference Include="System.EnterpriseServices" />
    <Reference Include="System.Web.Mobile" />
    <Reference Include="System.Xml.Linq" />
  </ItemGroup>
  <ItemGroup>
    <Content Include="Default.aspx" />
    <Content Include="Web.config" />
  </ItemGroup>
  <ItemGroup>
    <Compile Include="Default.aspx.cs">
      <SubType>ASPXCodeBehind</SubType>
      <DependentUpon>Default.aspx</DependentUpon>
    </Compile>
    <Compile Include="Default.aspx.designer.cs">
      <DependentUpon>Default.aspx</DependentUpon>
    </Compile>
    <Compile Include="Properties\AssemblyInfo.cs" />
  </ItemGroup>
  <ItemGroup>
    <Content Include="..\..\attachments.pdf">
      <Link>attachments.pdf</Link>
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </Content>
  </ItemGroup>
  <PropertyGroup>
    <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">10.0</VisualStudioVersion>
    <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>
  </PropertyGroup>
  <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
  <Import Project="$(VSToolsPath)\WebApplications\Microsoft.WebApplication.targets" Condition="'$(VSToolsPath)' != ''" />
  <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\WebApplications\Microsoft.WebApplication.targets" Condition="false" />
  <!-- To modify your build process, add your task inside one of the targets below and uncomment it. 
       Other similar extension points exist, see Microsoft.Common.targets.
  <Target Name="BeforeBuild">
  </Target>
  <Target Name="AfterBuild">
  </Target>
  -->
  <ProjectExtensions>
    <VisualStudio>
      <FlavorProperties GUID="{349c5851-65df-11da-9384-00065b846f21}">
        <WebProjectProperties>
          <UseIIS>False</UseIIS>
          <AutoAssignPort>True</AutoAssignPort>
          <DevelopmentServerPort>54471</DevelopmentServerPort>
          <DevelopmentServerVPath>/</DevelopmentServerVPath>
          <IISUrl>
          </IISUrl>
          <NTLMAuthentication>False</NTLMAuthentication>
          <UseCustomServer>False</UseCustomServer>
          <CustomServerUrl>
          </CustomServerUrl>
          <SaveServerSettingsInUserFile>False</SaveServerSettingsInUserFile>
        </WebProjectProperties>
      </FlavorProperties>
    </VisualStudio>
  </ProjectExtensions>
</Project>
```

<!-- code block end -->    

<!-- code block begin -->

##### ****ExtractAttachments.sln:**
    
```

Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 2013
VisualStudioVersion = 12.0.40629.0
MinimumVisualStudioVersion = 10.0.40219.1
Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "ExtractAttachments", "ExtractAttachments.csproj", "{A8705DB2-82C7-46E7-8786-058EEE78DE9D}"
EndProject
Global
	GlobalSection(SolutionConfigurationPlatforms) = preSolution
		Debug|Any CPU = Debug|Any CPU
		Release|Any CPU = Release|Any CPU
	EndGlobalSection
	GlobalSection(ProjectConfigurationPlatforms) = postSolution
		{A8705DB2-82C7-46E7-8786-058EEE78DE9D}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
		{A8705DB2-82C7-46E7-8786-058EEE78DE9D}.Debug|Any CPU.Build.0 = Debug|Any CPU
		{A8705DB2-82C7-46E7-8786-058EEE78DE9D}.Release|Any CPU.ActiveCfg = Release|Any CPU
		{A8705DB2-82C7-46E7-8786-058EEE78DE9D}.Release|Any CPU.Build.0 = Release|Any CPU
	EndGlobalSection
	GlobalSection(SolutionProperties) = preSolution
		HideSolutionNode = FALSE
	EndGlobalSection
EndGlobal

```

<!-- code block end -->    

<!-- code block begin -->

##### ****Web.config:**
    
```
<?xml version="1.0"?>
<configuration>
  <appSettings/>
  <connectionStrings/>
  <system.web>
    <!-- 
            Set compilation debug="true" to insert debugging 
            symbols into the compiled page. Because this 
            affects performance, set this value to true only 
            during development.
        -->
    <compilation debug="true" targetFramework="4.0"/>
    <!--
            The <authentication> section enables configuration 
            of the security authentication mode used by 
            ASP.NET to identify an incoming user. 
        -->
    <authentication mode="Windows"/>
    <!--
            The <customErrors> section enables configuration 
            of what to do if/when an unhandled error occurs 
            during the execution of a request. Specifically, 
            it enables developers to configure html error pages 
            to be displayed in place of a error stack trace.

        <customErrors mode="RemoteOnly" defaultRedirect="GenericErrorPage.htm">
            <error statusCode="403" redirect="NoAccess.htm" />
            <error statusCode="404" redirect="FileNotFound.htm" />
        </customErrors>
        -->
    <pages controlRenderingCompatibilityVersion="3.5" clientIDMode="AutoID"/>
  </system.web>
</configuration>
```

<!-- code block end -->