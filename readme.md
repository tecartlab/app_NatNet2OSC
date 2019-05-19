NatNet2OSC
===================================


NatNet2OSC is a small app designed to convert the Optitrack NatNet 2.0 protocoll to Open Sound Control (OSC). It provides the following features:

+ connects ...
+ Sends an OSC Packet from NatNet Packet.
+ Receive OSC packets via UDP.

Download
--------

https://github.com/tecartlab/app_NatNet2OSC/releases

License
-------

NatNet2OSC is licensed under the MIT license.

See License.txt

Using The Application
-----------------

Usage:  NatNet2OSC <OSCIP (localIP)> <OSCPort (54321)>  <MultCast (castIP)> <oscMode (max=1, isadora=2, touch=4, max+touch=5, etc]> <UpAxis 0=same, 1=yUp to zUp> <verbose [0/1]> <legacy [0/1]>

If Motive is streaming with the UpAxis = yUp you can transform it to zUp by setting the UpAxis = 1.

streaming the following messages are sent depending on the OSC Mode

+ /frame/start \<frameNumber>

MAX/MSP: OSC MODE = 1

+ /rigidbody \<rigidbodyID> tracked \<0/1>
+ /rigidbody \<rigidbodyID> position \<x> \<y> \<z>
+ /rigidbody \<rigidbodyID> quat \<qx> \<qy> \<qz> \<qw>

+ /skeleton/bone \<skleletonName> \<boneID> position \<x> \<y> \<z>
+ /skeleton/bone \<skleletonName> \<boneID> quat \<qx> \<qy> \<qz> \<qw>
+ /skeleton/joint \<skleletonName> \<boneID> quat \<qx> \<qy> \<qz> \<qw>

ISADORA: OSC MODE = 2

+ /rigidbody/\<rigidbodyID>/tracked \<0/1>
+ /rigidbody/\<rigidbodyID>/position \<x> \<y> \<z>
+ /rigidbody/\<rigidbodyID>/quat \<qx> \<qy> \<qz> \<qw>

+ /skeleton/\<skleletonName>/bone/\<boneID>/position \<x> \<y> \<z>
+ /skeleton/\<skleletonName>/bone/\<boneID>/quat \<qx> \<qy> \<qz> \q<w>
+ /skeleton/\<skleletonName>/joint/\<boneID>/quat \<qx> \<qy> \<qz> \<qw>

TouchDesigner: OSC MODE = 4

+ /rigidbody/\<rigidbodyID>/tracked \<0/1>
+ /rigidbody/\<rigidbodyID>/transformation \<x> \<y> \<z> \<qx> \<qy> \<qz> \<qw>

+ /skeleton/\<skleletonName>/bone/\<boneID>/transformation \<x> \<y> \<z> \<qx> \<qy> \<qz> \<qw>
+ /skeleton/\<skleletonName>/joint/\<boneID>/quat \<x> \<y> \<z> \<w>

IF you want to have multiple modes, set the oscmode for "max and isadora (1+2)" to 3 or "isadora and touch (2+4)" to 6

At the end of the frame the frameend message is sent

+ /frame/end \<frameNumber>


Building
---------

This code is based on the NatNet SDK from optitrack (http://optitrack.com/downloads/developer-tools.html)

Open the NatNetSamples inside the /Samples - folder and build NatNet2OSC Project

Contribute
----------

I would love to get some feedback. Use the Issue tracker on Github to send bug reports and feature requests, or just if you have something to say about the project. If you have code changes that you would like to have integrated into the main repository, send me a pull request or a patch. I will try my best to integrate them and make sure NatNetThree2OSC improves and matures.
