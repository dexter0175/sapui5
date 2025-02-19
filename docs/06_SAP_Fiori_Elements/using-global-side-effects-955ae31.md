<!-- loio955ae316856a4dcdbe07a1dbf584fa98 -->

# Using Global Side Effects

Global side effects are those side effects that are defined without any source properties or source entities.

We recommend that you use [SAP Fiori tools](https://help.sap.com/viewer/product/SAP_FIORI_tools/Latest/en-US), which is a set of extensions for SAP Business Application Studio and Visual Studio Code, to build your apps.

> ### Note:  
> Global side effecst are only applicable to draft-enabled applications.

Global side effects can be annotated under each entity separately. When you press [Enter\] on any input field, the global side effect defined under the corresponding entity is triggered.

The following sample code shows the global side effect with target fields and the `TriggerAction`:

> ### Sample Code:  
> XML Annotation
> 
> ```xml
> 
> <Annotations Target="NAMESPACE.ENTITYTYPE">
>     <Annotation Term="com.sap.vocabularies.Common.v1.SideEffects" Qualifier="GlobalSideEffect">
>         <Record>
>             <PropertyValue Property="TargetProperties">
>                 <Collection>
>                     <String>TaxAmount</String>
>                     <String>NetAmount</String>
>                     <String>GrossAmount</String>
>                 </Collection>
>             </PropertyValue>
>           <PropertyValue Property="TriggerAction" String="NAMESPACE.MyAction"/>
>         </Record>
>     </Annotation>
> </Annotations>
> 
> ```



<a name="loio955ae316856a4dcdbe07a1dbf584fa98__section_b5t_bn1_twb"/>

## Additional Features in SAP Fiori Elements for OData V2

If the `TriggerAction` is annotated with a global side effect, then on pressing [Enter\] the `TriggerAction` replaces the `PreparationAction` call. For more information, see [Draft Handling](draft-handling-ed9aa41.md).

To optimize performance, make the annotations for the desired side effects as specific as possible.

It is recommended to specify the target properties or target entities for global side effects. For exceptional cases, apps can configure to refresh the whole entity with the help of the `forceGlobalRefresh` parameter in the `manifest.json`.

> ### Sample Code:  
> `manifest.json`
> 
> ```
> "sap.ui.generic.app": {
>         "_version": "1.3.0",
>         "settings": {
>             "forceGlobalRefresh": true,
>             .....
>                 }
>             },
> ```

-   If the `forceGlobalRefresh` parameter is set to `true`, a refresh of the entire model is triggered when you press [Enter\].

-   If the parameter is set to `false`, then only the annotated targets are refreshed, and/or the annotated `TriggerAction` is called.

-   As of SAPUI5 1.106, if the parameter is not set, the \(runtime\) default is `false`.


For newly generated apps, the \(design time\) default is `false`, that is, the project generation wizard generates `"forceGlobalRefresh": false`.

We recommend that you use [SAP Fiori tools](https://help.sap.com/viewer/product/SAP_FIORI_tools/Latest/en-US), which is a set of extensions for SAP Business Application Studio and Visual Studio Code, to build your apps. You can also use SAP Web IDE.

> ### Caution:  
> SAP Web IDE is no longer available via SAP Business Technology Platform trial accounts. Any references to SAP Web IDE in this documentation are only relevant for you if you have access to SAP Web IDE through a productive SAP BTP account. Please consider SAP Business Application Studio as an alternative. See [App Development Using SAP Business Application Studio](../05_Developing_Apps/app-development-using-sap-business-application-studio-6bbad66.md).

For more information about SAP Web IDE, see the documentation for SAP Web IDE on the SAP Help Portal at [https://help.sap.com/viewer/p/SAP\_Web\_IDE](https://help.sap.com/viewer/p/SAP_Web_IDE).



<a name="loio955ae316856a4dcdbe07a1dbf584fa98__section_hkm_hzq_5wb"/>

## Additional Features in SAP Fiori Elements for OData V4

The following CAP CDS sample code shows the global side effect with target fields and the `TriggerAction`:

> ### Sample Code:  
> CAP CDS Annotation
> 
> ```
> 
> annotate NAMESPACE.ENTITYTYPE @(
> Common.SideEffects #GlobalSideEffect : {
>     TargetProperties : [
>         TaxAmount,
>         NetAmount,
>         GrossAmount
>     ]
>     TriggerAction : 'NAMESPACE.MyAction'
> }
> );
> ```

**Related Information**  


[Draft Handling](draft-handling-ed9aa41.md "A draft is an interim version of a business entity that has not yet been explicitly saved as an active version. Drafts are saved automatically in the background whenever users add or change information within a business entity while it's in edit mode (auto-save). SAP Fiori elements support the creation of apps using draft handling.")

