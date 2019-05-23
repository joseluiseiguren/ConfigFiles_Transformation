Web
---
	Agregar en el Configuration manager, una configuracion por environment
	Agregar un publish profile por environment
	Poner lo custom de cada environment en cada web.config



Console
-------
	Add to csproj before close tag </Project>:
		<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
		<UsingTask TaskName="TransformXml" AssemblyFile="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\Web\Microsoft.Web.Publishing.Tasks.dll" />
		<Target Name="BeforeBuild" Condition="exists('App.$(Configuration).config')">
			<TransformXml Source="App.config" Destination="$(IntermediateOutputPath)$(TargetFileName).config" Transform="App.$(Configuration).config"/>	
		</Target>

	To include config file inside general app.config
		<None Include="App.config" />
		<None Include="App.Release-QA.config">
			<DependentUpon>App.config</DependentUpon>
		</None>