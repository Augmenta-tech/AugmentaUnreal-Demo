# [Augmenta](https://www.augmenta-tech.com) [Unreal](https://www.unrealengine.com) Demo

This Unreal 5.1 project contains the [Augmenta Unreal plugin](https://github.com/Augmenta-tech/AugmentaUnreal) and a sample map with a Blueprint to test the plugin.

## Files for Testing

 - `Content/Maps/AugmentaDemo.umap` : This map contains the `BP_AugmentaTest` actor for testing.
 - `Content/Blueprints/BP_AugmentaTest.uasset` : A test blueprint actor that has the `Receive Ip Address` and `Port` variables exposed for modification. The default values are `127.0.0.1` and `12000` respectively. This actor also has the following functionality.
 	- On Actor BeginPlay : Creates an AugmentaReceiver that in turn connects to the OSCServer with the given Ip address and Port and also binds to the Augmenta Plugin events i.e., `OnSceneUpdated`, `OnObjectEntered`, `OnObjectUpdated`, `OnObjectLeft`, `OnVideoOutputUpdated`, `OnEnteredExtraData`, `OnUpdatedExtraData` and `OnLeaveExtraData`.
	- It contains a cube called PlayArea which is scaled according to the AugmentaScene data when `OnSceneUpdated` event fires.
	- It creates a `Sphere` when `OnObjectEntered` event fires and updates its position relative to the PlayArea using the AugmentaPerson data. It uses a map to track the AugmentaPerson with the `Id` as the key and the sphere static mesh component as the value.
	- When `OnObjectUpdated` event is fired, a sphere is created if the AugmentaPerson has not been tracked before. Otherwise, will update the relative position of the already existing sphere according to the Id.
	- It removes the sphere when `OnObjectLeft` event fires.
	- When `OnVideoOutputUpdated` event is fired, currently it just logs the data (offset, size and resolution) to the screen.
	- When `OnEnteredExtraData` or `OnUpdatedExtraData` or `OnLeaveExtraData` event is fired, currently it just logs the Id of the object to the screen.
	- On Actor EndPlay : Stops the AugmentaReceiver that in turn stops the connection to the OSCServer.

## How to Test

There are 2 ways to test this Demo.
 1. Using the Physical Augmenta Nodes that send data to an AugmentaFusion software on a PC and using the IP address of that PC as the `Receive Ip Address`.
 2. Using the [AugmentaSimulator](https://github.com/Augmenta-tech/Augmenta-Simulator/releases). The default output Ip address and Port in the Augmenta simulator are set to `127.0.0.1` and `12000` respectively. So the demo should work without any modifications.
