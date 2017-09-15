# MatrixHelper
A simple swift struct to help you augment AR anchor positions in 3D space.

### Examples

In your Scene.swift file - Given your standard transform:

```swift
override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
        
   guard let sceneView = self.view as? ARSKView else {
       return
   }
   // Create anchor using the camera's current position
   if let currentFrame = sceneView.session.currentFrame {
        // put anchor 3 meters ahead of you
        var zTranslation = matrix_identity_float4x4
        zTranslation.columns.3.z = -3.0
        let transform = simd_mul(currentFrame.camera.transform, zTranslation)
        
        // we will do stuff to the transform here...
        
        let anchor = ARAnchor(transform: transform)
        sceneView.session.add(anchor: anchor)
   }
}
```
You can force that anchor to the horizon line:
```swift
let resetToHorizon = MatrixHelper.resetToHorizon(transform)
```
You can move it left or right by x degrees:
```swift
let toTheLeft = MatrixHelper.rotateMatrixAroundY(degrees: 45.0, matrix: transform)
```
You can move it up or down by x degrees:
```swift
let moveDown = MatrixHelper.translateMatrixFromHorizon(degrees: -10.0, matrix: transform)
```

Enjoy!
