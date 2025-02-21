# maui_blazor_prueba

# Preparando lso Certificados.

## provisional profile
se genera el fichero Provisional profile ".mobilprovision""

   1- registro de un nuevo didentificador     
            access wifi- information 
            communication notifications
            push notifications

   2- alta del profiles de distribuci�n
            App Store Connect> 
            
            Certificados, Identificadores y Perfiles>Distribution >App Store Connect
                     create a distribution provsiona

            Seleecionar un app id (paso anterior)

            seleccionar el certificado de distribucion 

            Review, Name and Generate: es el mismo que el del paquete 


# Configuracion del respositorio


1- configurar el secrets.

en configuracion / Security / Secrets and variables / Actions > Pesta�a secretos.

IOS_CERT_DIST_CONTAIN_BASE64 = contenido en base 64 del certificado de distribuci�n.


2- token de securidad

en settings / developer settins > tokens (classics)

repo > public_repo_      V


GITHUB_TOKEN

Aquí tienes la tabla actualizada en formato Markdown, incluyendo las versiones mínimas de iOS compatibles y las versiones de .NET correspondientes:  

```markdown
| Versión de Xcode(*) | Versión del SDK de iOS | Versiones de iOS Compatibles | Versión Mínima de iOS*| Versión de .NET (*) |
|---------------------|------------------------|------------------------------|-----------------------|---------------------|
| 16.0                | 18.0                   | 18.0                         | 14.0                  | .NET 9.0            |
| 15.0                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 14.0                | 16.0                   | 16.0                         | 12.0                  | .NET 7.0            |
| 13.0                | 15.0                   | 15.0                         | 11.0                  | .NET 6.0            |
| 12.0                | 14.0                   | 14.0                         | 10.0                  | .NET 6.0            |
| 11.0                | 13.0                   | 13.0                         | 9.0                   | .NET 5.0            |
| 10.0                | 12.0                   | 12.0                         | 9.0                   | .NET 5.0            |
| 9.0                 | 11.0                   | 11.0                         | 9.0                   | Xamarin.iOS 14.x    |
| 8.0                 | 10.0                   | 10.0                         | 8.0                   | Xamarin.iOS 13.x    |
| 7.0                 | 9.0                    | 9.0                          | 8.0                   | Xamarin.iOS 12.x    |
| 6.0                 | 8.0                    | 8.0                          | 7.0                   | Xamarin.iOS 11.x    |
```

| 16.2                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 16.2.0              | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 16.1                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 16.1.0              | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.4                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.4.0              | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.3                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.3.0              | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.2                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.1                | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |
| 15.0.1              | 17.0                   | 17.0                         | 13.0                  | .NET 8.0            |



Si necesitas más cambios o información adicional, ¡avísame!

compatibilidades:
https://learn.microsoft.com/es-es/dotnet/maui/supported-platforms?view=net-maui-9.0



```
dotnet publish "$PROJECT_BUILD_FILE_PATH" -c $BUILD_CONFIG -f:${DOTNET_VERSION_TARGET}-ios --p:ArchiveOnBuild=true \
  --p:EnableAssemblyILStripping=false --p:CodesignKey="$CERT_DIST_NAME" \
  --p:CodesignProvision="com.pruebablazor9.mobileprovision"
 

```
xcodebuild -exportArchive \
  -archivePath "/Users/runner/work/maui_blazor_prueba/maui_blazor_prueba/PruebaBlazor/PruebaBlazor8/ios/archive/PruebaBlazor8.xcarchive" \
  -exportOptionsPlist "/Users/runner/work/maui_blazor_prueba/maui_blazor_prueba/PruebaBlazor/PruebaBlazor8/ios/ExportOptions.plist" \
  -exportPath "/Users/runner/work/maui_blazor_prueba/maui_blazor_prueba/PruebaBlazor/PruebaBlazor8/ios/ipa"
```

```
   ls -l "/Users/runner/Library/MobileDevice/Provisioning\ Profiles/"

   uuid=$(security cms -D -i "/Users/runner/Library/MobileDevice/Provisioning\ Profiles/compruebablazor9.mobileprovision" \
   grep -A1 "<key>UUID</key>" | tail -n1 | sed -e 's/<[^>]*>//g' | tr -d '[:space:]')
   echo "UUID: $uuid" 


   dotnet msbuild "/Users/runner/work/maui_blazor_prueba/maui_blazor_prueba/PruebaBlazor/PruebaBlazor8/PruebaBlazor8.csproj" \
   /t:Publish \
   /p:Configuration=Release \
   /p:Platform=iPhone \
   /p:TargetFramework=net8.0-ios \
   /p:RuntimeIdentifier=ios-arm64 \
   /p:ArchiveOnBuild=true \
   /p:EnableAssemblyILStripping=false \
   /p:CodesignKey="Apple Distribution: NOTIONS GROUP S.A. (8BU3XBJR6T)" \
   /p:CodesignProvision="$uuid"
```


# /p:CodesignProvision="com.pruebacertificado" \