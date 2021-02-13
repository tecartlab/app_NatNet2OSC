NatNet2OSC 8.2
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

**Usage:  NatNet2OSC <OSCIP (localIP)> <OSCPort (54321)>  <MultCast (castIP)> <oscMode (max=1, isadora=2, touch=4, max+touch=5, etc]> <UpAxis 0=same, 1=yUp to zUp> <verbose [0/1]> <legacy [0/1]>**

example streaming the 'sparck' mode with transform yUp to zUp:

    NatNet2OSC 192.168.2.2 54321 54322 239.255.42.99 8 1 0 0

If Motive is streaming with the UpAxis = yUp you can transform it to zUp by setting the UpAxis = 1.

streaming the following messages are sent depending on the OSC Mode

+ /frame/start \<frameNumber>
+ /frame/timestamp \<ms since Day Started(float)>

in case of SPARCK: OSC MODE = 8
+ /f/s \<frameNumber>
+ /f/t \<ms since Day Started(float)>


MAX/MSP: OSC MODE = 1

+ /rigidbody \<rigidbodyID> tracked \<0/1>
+ /rigidbody \<rigidbodyID> position \<x> \<y> \<z>
+ /rigidbody \<rigidbodyID> quat \<qx> \<qy> \<qz> \<qw>

+ /skeleton/bone \<skleletonID> \<boneID> position \<x> \<y> \<z>
+ /skeleton/bone \<skleletonID> \<boneID> quat \<qx> \<qy> \<qz> \<qw>
+ /skeleton/joint \<skleletonID> \<boneID> quat \<qx> \<qy> \<qz> \<qw>

ISADORA: OSC MODE = 2

+ /rigidbody/\<rigidbodyID>/tracked \<0/1>
+ /rigidbody/\<rigidbodyID>/position \<x> \<y> \<z>
+ /rigidbody/\<rigidbodyID>/quat \<qx> \<qy> \<qz> \<qw>

+ /skeleton/\<skleletonID>/bone/\<boneID>/position \<x> \<y> \<z>
+ /skeleton/\<skleletonID>/bone/\<boneID>/quat \<qx> \<qy> \<qz> \q<w>
+ /skeleton/\<skleletonID>/joint/\<boneID>/quat \<qx> \<qy> \<qz> \<qw>

TouchDesigner: OSC MODE = 4

+ /rigidbody/\<rigidbodyID>/tracked \<0/1>
+ /rigidbody/\<rigidbodyID>/transformation \<x> \<y> \<z> \<qx> \<qy> \<qz> \<qw>

+ /skeleton/\<skleletonID>/bone/\<boneID>/transformation \<x> \<y> \<z> \<qx> \<qy> \<qz> \<qw>
+ /skeleton/\<skleletonID>/joint/\<boneID>/quat \<x> \<y> \<z> \<w>

SPARCK: OSC MODE = 8

+ /rb \<rigidbodyID> \<datatype = 1> \<markerId> \<x> \<y> \<z>
+ /rb \<rigidbodyID> \<datatype = 2> \<timestamp> \<x> \<y> \<z> \<qx> \<qy> \<qz> \<qw>
+ /skel \<skleletonID> \<datatype = 10> \<boneID> \<timestamp> \<x> \<y> \<z> \<qx> \<qy> \<qz> \<qw>

AMBI: OSC MODE = 16

+ /icst/ambi/sourceindex/xyz \<rigidbodyID> \<x> \<y> \<z>

IF you want to have multiple modes, set the oscmode for "max and isadora (1+2)" to 3 or "isadora and touch (2+4)" to 6

At the end of the frame the frameend message is sent

+ /frame/end \<frameNumber>

in case of SPARCK: OSC MODE = 8

+ /f/e \<frameNumber>

### Remote control

sending commands to the \<OscCmndPort> will pass commands to Motive:

the following commands are implemented:

    /motive/command refetch

will return all rigidbodies and skeletons currently streaming

+ /motive/update/start
+ /motive/rigidbody/id \<rigidbodyName> \<rigidbodyID>
+ /motive/skeleton/id \<skleletonName> \<SkeletonID>
+ /motive/skeleton/id/bone \<skleletonName> \<boneID> \<boneName>
+ /motive/update/end

Building
---------

This code is based on the NatNet SDK from optitrack (http://optitrack.com/downloads/developer-tools.html)

and http://www.rossbencina.com/code/oscpack

Contribute
----------

I would love to get some feedback. Use the Issue tracker on Github to send bug reports and feature requests, or just if you have something to say about the project. If you have code changes that you would like to have integrated into the main repository, send me a pull request or a patch. I will try my best to integrate them and make sure NatNetThree2OSC improves and matures.
