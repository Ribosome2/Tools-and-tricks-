# Tools-and-tricks-
开发过程中遇到的一些技巧和 工具记录

1：在VisualStudio中添加代码模版：
这里我们以添加Lua模版为例子
（1）这里是官方的说明，https://msdn.microsoft.com/en-us/library/tsyyf0yh.aspx
虽然有了官方文档，但是总有些问题
这里讲下基本步骤：
1)建一个lua工程
2)创建一个.lua 文件 随意编辑这个lua文件为我们想要的模版内容
3）菜单栏工具：文件-->导出模版-->项模版-->一直点到完成
  最后会看到文件系统默认导出我们命名的.zip文件到了
  C:\Users\Administrator\Documents\Visual Studio 2012\My Exported Templates\template1.zip（templates1就是你自己命名的）
坑爹的是 这个并不是最终在VS中起效的文件
要让它们生效，我们要修改的文件在这个目录下：C:\Users\Administrator\Documents\Visual Studio 2012\Templates\ItemTemplates
解压template1.zip可以看到里面有.lua文件，和.vstemplate文件
模版内容可以通过修改.lua文件，但是作为模版文件必须要让它可以自动替换一些变量，比如时间，文件名，用户名这样的东西
但是我并没有看到导出的时候开启“替换变量”的开关。需要修改.vstemplate文件才可以替换
例子：
<VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
  <TemplateData>
    <DefaultName>template1.lua</DefaultName>
    <Name>template1</Name>
    <Description>&lt;没有可用的说明&gt;</Description>
    <ProjectType>Lua</ProjectType>
    <SortOrder>10</SortOrder>
    <Icon>__TemplateIcon.ico</Icon>
  </TemplateData>
  <TemplateContent>
    <References />
    <ProjectItem TargetFileName="$fileinputname$.lua" ReplaceParameters="true">LuaFile1.lua</ProjectItem>
    <ProjectItem ReplaceParameters="true">LuaFile1.lua</ProjectItem>
  </TemplateContent>
</VSTemplate>


其中：“ <ProjectItem ReplaceParameters="true">LuaFile1.lua</ProjectItem>”这一行是我们要加进去的（LuaFile.lua是我们导出模版时候的文件名）

修改好之后，保存到压缩文件中，就看到该有的模版起效果了
