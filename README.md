# Augmenta Unreal Demo

This Unreal (4.24) project contains the `Augmenta Unreal Plugin` and a sample map with a Blueprint to test the plugin.

## Files for Testing

 - `Content/Maps/AugmentaDemo.umap` : This map contains the `BP_AugmentaTest` actor for testing.
 - `Content/Blueprints/BP_AugmentaTest.uasset` : A test blueprint actor that has the `Receive Ip Address` and `Port` variables exposed for modification. The default values are `127.0.0.1` and `12000` respectively. This actor also has the following functionality.
 	- On Actor BeginPlay : Creates an AugmentaReceiver that in turn connects to the OSCServer with the given Ip address and Port and also binds to the Augmenta Plugin events i.e., `OnSceneUpdated`, `OnPersonEntered`, `OnPersonUpdated` and `OnPersonWillLeave`.
	- It contains a cube called PlayArea which is scaled according to the AugmentaScene data when `OnSceneUpdated` event fires.
	- It creates a `Sphere` when `OnPersonEntered` event fires and updates its position relative to the PlayArea using the AugmentaPerson data. It uses a map to track the AugmentaPerson with the Pid as the key and the sphere static mesh component as the value.
	- When `OnPersonUpdated` event is fired, a sphere is created if the AugmentaPerson has not been tracked before. Otherwise, will update the relative position of the already existing sphere according to the Pid.
	- It removes the sphere when `OnPersonWillLeave` event fires.
	- On Actor EndPlay : Stops the AugmentaReceiver that in turn stops the connection to the OSCServer.

## How to Test

There are 2 ways to test this Demo.
 1. Using the Physical Augmenta Nodes that send data to an AugmentaFusion software on a PC and using the IP address of that PC as the `Receive Ip Address`.
 2. Using the [AugmentaSimulator](https://github.com/Theoriz/Augmenta-Simulator/releases). The default output Ip address and Port in the Augmenta simulator are set to `127.0.0.1` and `12000` respectively. So the demo should work without any modifications.
