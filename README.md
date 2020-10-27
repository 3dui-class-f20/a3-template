# Assignment 3:  Better Teleportation

In this assignment, you will implement an alternative version of teleportation. As with A2, you may implement this using any of the 3 environments from Assignment 1 (Babylon.js, Playcanvas Editor, or Playcanvas Engine).  You may reuse any of your code from previous assignments. This template is empty (except for a .gitignore file and this README.md);  you should fill in the project with something similar to 1(a), 1(b), or 1(c) and follow the corresponding instructions for submission.

The goal of the assignment is to have you experiment with variations of teleportation that have slightly different visual behaviors.  Secondary goals include dealing with interaction state over multiple frames, implementing smooth motion, and more 3D interaction programming.

The two variations are described in this [YouTube Video of Locomotion in Half-Life: Alyx (HL:A)](https://www.youtube.com/watch?v=TX58AbJq-xo)(I've put the video [on Purusall as well](https://app.perusall.com/courses/3d-user-interfaces/_/dashboard/documents/folder-ZAaNqTWeCPMhJwHkP)).  While the specifics are discussed below, the two techniques are:
- Blink Teleport.  Teleportation where you move immediately to the target location. The basic implementation, used in the Playcanvas starter kit, for example. For this variation, you must implement the HL:A refinement, where screen goes black before movement for a short time, and then fades out of black over a short time.  
- Shift Teleport.  Teleportation where you move smoothly to the target location over a short time. 

![HL:A Locomotion Modes](/resources/hl-alyx-movement.png)

## Due: Monday November 9th, 11:59pm (midnight)

## Name and GT user-id

Name: 
User ID:
Playcanvas Username (if appropriate): 

## Additional Details 

The goal of the assignment is to implement the two teleportation techniques, and create a small test environment to use them in.  If you are using Babylon, you should disable the default movement controls and implement your own. (In either Babylon or Playcanvas, you should implement the controls inside your application without worrying about making the movement controls be "integrated" in the system like Babylons controls.)

You should satisfy the following overall constraints.

- create a space big enough to test the teleportation techniques.  You could use either the Babylon default space or the Playcanvas space from the WebXR Sample.  You only need to teleport on a single flat floor plane, not multiple surfaces or objects.
- distribute objects of different sizes and appearances around the space (cubes and other shapes, models, etc.).  Make sure there are a reasonable number of objects with different sizes. Visual complexity will make the teleportation techniques easier to experience more realistically.
- the controllers should have visual feedback as to where the teleport will go (ray or arc, circular image or object indicating landing position at the intersection of the floor).
- clicking the controller trigger should teleport using the method on that controller.
- use one controller to move around the scene using Blink Teleport, and the other controller to move around using Shift Teleport.
- display a single text label attached to each of the controllers. The Blink controller shows "Fade: 0.1 s" initially, the Shift controller shows "Slide: 0.5 s" initially.  These is the timing values used by the two techniques.
- when the user pushes forward/up on one of the thumbsticks on each controller (your choice which, could be all of them or just one), the value for that controller/technique should double (0.1 to 0.2 to 0.4 to 0.8, etc). Each push forward should increase once. When the user pulls backward/down on the same stick, the value halve (0.1 to 0.05 to 0.025, etc). The text label should change appropriately.

### Blink Teleport

There are two components to this modified version of Blink Teleport, compared to what is implemented in most systems: making the screen black before moving the user, and then fading from black to the regular view after moving the user.  

There are various approaches you could take to making the screen black and fading in the scene at the new location. First, you could set up a post-processing filter (both Babylon and Playcanvas support multi-pass rendering) that fades the scene from black to full color over the current "Fade" time, after holding the camera black for a small fixed time.

A second simple approach is to create a black plane and position it so it covers the camera views of the scene, and then fade it from fully opaque to fully transparent over the "Fade" time.  Ideally, you would need the plane to be right at the near clipping plane (a close to the viewer as it could be such that other things close to the user are not visible), but it's more likely in a production system (where the teleport technique is fully integrated), you would just not draw anything.  So, for this assignment, putting a plane a few inches in front of the head position such that it sits in front of their two eye positions is sufficient;  you will want to experiment to get this just right.

Either approach is fine for this assignment.

You should make the initial period of full black very short (perhaps 1/25th of a second or so).  As with all animations, you should base this time period on time, not on a number of rendering frames, to ensure it behaves similarly on displays with different frame rates.

### Shift Teleport

Shift Teleport opts to rapidly move the user to the target location, instead of instantly moving them.  The "Slide" value is the time it takes to move to the target location.  When the user selects a target location, the motion should linearly move from the start to the end over the "Slide" time value (e.g., 0.1 s).

## Rubric

Graded out of 10.

1. Your project runs locally using `npm run start` (1)
2. At least 10 objects of at least 3 types created around the scene of different sizes and distances from the user's starting point. (1)
3. One teleport control and label on each controller. (1)
4. Teleportation visual feedback on each controller. (1)
4. Teleport using appropriate technique when trigger pressed. (1)
5. Thumbstick doubles and halves Fade and Slide time correctly on each controller. (1)
6. Blink: screen goes black for short time, fades from black to full color over "Fade" time. (2)
7. Shift: user moves smoothly to the target location over the appropriate amount of time. (2)

Up to two bonus points can be received for doing the following (1 each) enhancements to the Slide Teleport:
- during the "Slide" movement, you should shrink the field of view the user sees by shrinking the visible scene using a field of view restrictor as illustrated [here](https://spectrum.ieee.org/tech-talk/consumer-electronics/gaming/dynamic-field-of-view-restriction-makes-virtual-reality-less-barfy).  Research has shown that this helps reduce motion sickness.   You should quickly zoom in the restrictor to cover part of the edge of the screen at the start of the motion, and zoom it back out after the motion is finished.
- use non-linear motion during the transition, moving slower at the beginning and end and quickly through the middle.

# Collaboration

You are free to discuss technical questions and issues in the Teams channels, but the code you submit should be your own.  So, please do not post large chunks of code, but providing pointers to examples or documentation pages or components and methods, along with discussion of how to use them, is fine.

# Submission

You will submit your assignment based on the instructions in 1(a), 1(b), or 1(c) (depending on if you used Babylon, Playcanvas Editor, or Playcanvas Engine, respectively.)

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Material for 3D User Interfaces Fall 2020</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.blairmacintyre.me/3dui-class-f20" property="cc:attributionName" rel="cc:attributionURL">Blair MacIntyre</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The intent of choosing (CC BY-NC-SA 4.0) is to allow individuals and instructors at non-profit entities to use this content.  This includes not-for-profit schools (K-12 and post-secondary). For-profit entities (or people creating courses for those sites) may not use this content without permission (this includes, but is not limited to, for-profit schools and universities and commercial education sites such as Corsera, Udacity, LinkedIn Learning, and other similar sites).   