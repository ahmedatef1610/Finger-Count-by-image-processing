# Finger-Count-by-image-processing

### Strategy for counting fingers
- Grab an ROI
- Calculate a running average background value for 60 frames of video
- Once avg value is found, then the hand can enter the ROI.
- Set an ROI and calculate the average running value for some amount of frames.
  - ![image](https://user-images.githubusercontent.com/39852784/127779454-11b470d9-8bbd-4995-afe3-cccf67fc9b67.png)
- Then once a hand enters, we can detect a change and apply thresholding.
  - ![ScreenShot_20210801191036](https://user-images.githubusercontent.com/39852784/127779582-56a0819c-f874-4018-83f5-605032d6416a.png)
- Once the hand enters the ROI, we will use a Convex Hull to draw a polygon around the hand.
  - ![image](https://user-images.githubusercontent.com/39852784/127779528-0430524d-271a-4c20-8383-3fa94259fb5d.png)
- Using some math, we ll calculate the center of the hand against the angle of outer points to infer finger count.
  - ![ScreenShot_20210801191120](https://user-images.githubusercontent.com/39852784/127779605-4108e7ec-7b63-4e2f-9b9f-426febb6ae72.png)
- First we will calculate the most extreme points (top, bottom, left, and right)
  - ![ScreenShot_20210801191458](https://user-images.githubusercontent.com/39852784/127779757-a48cb730-9b1f-45c1-847a-cf9af4d5fc91.png)
- We can then calculate their intersection and estimate that as the center of the hand
  - ![ScreenShot_20210801191515](https://user-images.githubusercontent.com/39852784/127779767-640eb86a-803f-4584-94c8-9d79338acf83.png)
- Next we will calculate the distance for the point furthest away from the center
  - ![ScreenShot_20210801191541](https://user-images.githubusercontent.com/39852784/127779790-0e98b63a-c074-4499-b7b9-93ffa114a68f.png)
- Then using a ratio of that distance we create a circle
  - ![ScreenShot_20210801191541](https://user-images.githubusercontent.com/39852784/127779793-ec5a22b9-0869-453b-a545-0a6b3431b9eb.png)
- Any points outside of this circle and far away enough from the bottom, should be extended fingers!
  - ![ScreenShot_20210801191541](https://user-images.githubusercontent.com/39852784/127779797-fa92ae7a-f3b0-4688-b46b-84e8044f6882.png)
