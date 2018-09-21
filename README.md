# vividFacesTrainHelper
Optional framework for creating landmark training source data.


iOS and some other modern mobiles all provide API for facial landmark detections (VNDetectFaceLandmarksRequest for iOS). It is a good train source for training tensorflow models.

But currently  VNDetectFaceLandmarksRequest is not good enough, it is slow and most important of all, lack of pupil center positions.
Until iOS 12, the output of left/right pupil center position is still the center of eyes. 
vividFacesTrainHelper uses API of OpenCV to detect the positions and for the one failed to get, return CGFloat.nan.
The Usage of vividFacesTrainHelper is quite simple and if the training of model is not required, the framework vividFacesTrainHelper is not necessary.
The framework canbe found at: https://github.com/zoonewbie/vividfaces/tree/master/vividFacesDemo/buildInFramework/vividFacesTrainHelper.framework

Check the GameViewController for detail

1.	import vividFacesTrainHelper//Optional
2.	declare a trainSource
``` 
var trainSrc : Landmark65TrainSrc?


 trainSrc = Landmark65TrainSrc()
```
3.	trainSrc can be the web images defined already in framework

```
let trainBlock : (UIImage, [[CGPoint]]) -> () = {(image: UIImage, normalizedPoints: [[CGPoint]]) -> () in
            self.gameController.trainImage(previewView: self.previewView, image:image, normalizedPoints: normalizedPoints)
            return
        }
        trainSrc!.trainWebImage(forTrain: trainBlock)
```        

4.	or an UIImage as input, and 65 normalizd points as output
```
let trainsrcBlock : (UIImage) -> ([[CGPoint]]?) = trainSrc!.trainImageBlock()
```

