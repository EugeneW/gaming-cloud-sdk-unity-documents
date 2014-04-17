# Getting Started

1.  Import the Unity Package "gaming-cloud-sdk-unity-v.*.*.*.unitypackage" of the Fresvii Gaming Cloud SDK. (Choose "Assets" > "Import Package" > "Custom Package...".)

2.  Lay out the Fresvii Gaming Cloud prefab to the scene.
![Layout prefab](./Images/InstallPrefab.png)

3.  In the Fresvii Gaming Cloud inspector, set the following app information.
![SetParametersInInspector](./Images/SetParametersInInspector.png)
|Data|Type|Description|
|-------|------|-----|
|App Icon|Texture2D|Image of the app icon|
|Host Url|string|Host URL of Fresvii Gaming Cloud|
|Uuid|string|App ID of Fresvii Gaming Cloud|
|GcmProjectId|string|Project ID when using the Google Cloud Messaging for Android service|
|Gcm Api Key|string|API key when using the Google Cloud Messaging for Android service|
When done with the settings of 1 to 3, you can use the methods of the FGC class.

4. To use the sample GUI, add the "FresviiSampleGUI" prefab to the scene.
![SetParametersInInspector](./Images/InstallPrefabGUI.png)