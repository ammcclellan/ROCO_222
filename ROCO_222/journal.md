# Journal

Markdown is a method of writing information, and using syntax to format that information. This is information can be converted directly into HTML.
--- 
## Syntax
+ using "#" will create headers. Increasing the number of "#'s" will reduce the size of the header.
+ typing ** ** or __ __ will create **bold** text.
+ typing _ _ or * * will create _italicised_ text.
+ through typing "-", "+" or "*" a bullet list can be created.
+ two spaces at the end of a line will create a one line break.
+ typing "---" will create a horizontal line, useful for separating information.
+ typing "1. 2. 3. etc " will create a numbered list.
+ typing "[link]""(the actual link)" (*without the "'s*).

## **Command-line 101**
___________________
___________________
The following bullets are commands that can be entered into a terminal to achieve a certain result and an overview of what those results are.
+ "$ ls" will list the directory contents.
+ "$ cd /tmp" will move to a temporary directory (using the RAM) this will be deleted after this session, however using the RAM will mean it is a lot faster.
+ the command "cd" will change directory.
bENCHMRK3242! trying to reach when using the "cd" command. e.g. "cd $HOME" is the same as cd "/students/home".
+ "mkdir" will make a directory.
+ "echo "*thing*"" will write thing. " echo "Hello" > hello.md" will make a document and write "hello" in that document.
+ "cat hello.md" will write out the contents of the document "hello".
+ cp hello.md hello-again.md will create a "hello-again doc" and copy the contents of "hello" into "hello-again".
+ "mv hello-again.md hello-hello.md" will rename "hello-again" to "hello-hello".
+ "rm hello.md" will remove the doc "hello".
+ "> hi.md" will create a doc called "hi".
+ "rm -rf" will remove files without question or inhibition repeatedly.
+ "cat /proc/cpuinfo" will display the info of the cpu.
+ typing "ls -al" will give you a detailed of all files in the directory

## DC Motors 

The first picture [Single Core Motor](https://photos.app.goo.gl/jvgf7CXRFyz7kxy13)


### Single Coil 
+ AIM:

- To know the key parts of a DC motor
- make a single coil dc motor


+ Parts for the motor:
[Parts of the Motor](https://photos.app.goo.gl/zTotbrEkya7QLOCD3)
- a cork
- copper tape
- a nail
- 4 neodymium magnets
- wooden base
- 4 paper clips
- copper coil


+ Procedure:
- insert the nail through both ends of the cork
- Commutator - stick 2 peices of copper tape on one end of the cork (make sure they don't touch)
- Armature - wind the wire around the cork and make sure both the ends are free
- Bend the paperclips to hold the magnets
- solder the ends of the coil to each piece of copper tape
- apply power to the commutator using wires by using the ends of the wires like brushes

#### Performance
[Single-Coil motor functioning](https://photos.app.goo.gl/a2n7oXHKw7K7IIfQ2)

The single-coil motor functioned reliably and to a fairly high standard.
The coil was made using copper wire wound 100 times making contact with the commutator.


### 4 Coil:

+ Procedure:

- Use Fusion 360 to design the armature and 3D print.
- Use FUsion 360 to design the magnet holders and print them.
- Wind 4 different coils around the armature 100 times each.
- Use four strips of copper tape to make the commutator.
- solder the ends of the wire to the copper tape.
- apply power to the commutator with copper wires.


#### Performance
[Four-Coil motor](https://photos.app.goo.gl/bK6Jy49uV1eum0AI2)

The functionality of our four core motor was unreliable at best. Only slightly rotating on occasion.
Upon reinserting the single coil armature into the same setup as the four coil, it became apparent that the motor's speed had reduced along with its reliability. 
By moving themagnet holders closer to the single coil motor, we were able to restore its functionality. 
The design of the armature was too wide. This meant that the magnets were not close enough to one another to gnerate a sufficent magnetic field to cause the motor to spin consistently.

+ Improvements: 
	There are many things that could have been done to improve our final four coil design
- the armature's design would have been more effect if the slots to wrap the coils around were slanted so as to further improve the speed of rotation of the motor.
- had we implemented the use of a metallic core (instead of a wooden one) the magneic field generated would have been stronger, increasing the effectiveness of the motor.
- redesigning the chasis: decreasing the size of the armature would have allowed us to move the magnets closer together and increasae the strength of the magnetic field, providing a more consistent rotation from the motor, hence allowing the calculation of rps and frequency.
___________________________________________
## Stepper Motors - partnered with IJaas
___________________________________________
+ Aim:
 - to understand what a stepper motor is
 - to be able to program a stepper motor using an arduino

+ Outline:
 - Stepper motors are synchronous electric motors.
 - By alternating which coils and wires the current flows through, a rotating magnetic field is generated, which in turn, turns the motor.

[Basic Stepper motor Video](https://photos.app.goo.gl/rzxW0PJFWqcTdBdG3)
[Improved Stepper Motor Video](https://photos.app.goo.gl/swYa62tRhpB8bzfo2)

+ Arduino code:
define DIR_A 12
define PWM_A 3
define DIR_B 13
define PWM_B 11

const int delayMs = 400;

void setup() {
pinMode(DIR_A, OUTPUT);
pinMode(DIR_B, OUTPUT);
pinMode(9, OUTPUT); digitalWrite(8, LOW); //No braking ch. A
pinMode(8, OUTPUT); digitalWrite(8, LOW); //No braking ch. B
}

void loop() {
  //full_step();
  //two_phase();
  half_step();
}

void full_step()
{

 digitalWrite(DIR_A, HIGH); // Ch. A forward
 digitalWrite(DIR_B, HIGH); // Ch. B forward
 analogWrite(PWM_A, 255); // Ch. A on
 analogWrite(PWM_B, 0); // Ch. B off
 delay(delayMs);
 
 analogWrite(PWM_A, 0); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delay(delayMs);
 
 digitalWrite(DIR_A, LOW); // Ch. A backwards
 digitalWrite(DIR_B, LOW); // Ch. B backwards
 analogWrite(PWM_A, 255); // Ch. A on
 analogWrite(PWM_B, 0); // Ch. B off
 delay(delayMs);
 
 analogWrite(PWM_A, 0); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delay(delayMs);
  
}


void two_phase()
{
   digitalWrite(DIR_A, HIGH); // Ch. A forward
 digitalWrite(DIR_B, HIGH); // Ch. B forward
 analogWrite(PWM_A, 255); // Ch. A on
 analogWrite(PWM_B, 255); // Ch. B off
delayMicroseconds(delayMs);
 
 digitalWrite(DIR_A, LOW);
 analogWrite(PWM_A, 255); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delayMicroseconds(delayMs);
 
 //digitalWrite(DIR_A, LOW); // Ch. A backwards
 digitalWrite(DIR_B, LOW); // Ch. B backwards
 analogWrite(PWM_A, 255); // Ch. A on
 analogWrite(PWM_B, 255); // Ch. B off
 delayMicroseconds(delayMs);
 
  digitalWrite(DIR_A, HIGH);
   //digitalWrite(DIR_B, HIGH);
 analogWrite(PWM_A, 255); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delayMicroseconds(delayMs);
}

void half_step()
{
 digitalWrite(DIR_A, HIGH); // Ch. A forward
 digitalWrite(DIR_B, HIGH); // Ch. B forward
 analogWrite(PWM_A, 255); // Ch. A on
 analogWrite(PWM_B, 0); // Ch. B off
delayMicroseconds(delayMs);
 
//digitalWrite(DIR_A, HIGH); // Ch. A forward
//digitalWrite(DIR_B, HIGH); // Ch. B forward
analogWrite(PWM_A, 255); // Ch. A off
analogWrite(PWM_B, 255); // Ch. B on
delayMicroseconds(delayMs);
 
 //digitalWrite(DIR_A, LOW); // Ch. A backwards
// digitalWrite(DIR_A, LOW); // Ch. B backwards
 analogWrite(PWM_A, 0); // Ch. A on
 analogWrite(PWM_B, 255); // Ch. B off
 delayMicroseconds(delayMs);
 
  digitalWrite(DIR_A, LOW);
   //digitalWrite(DIR_B, HIGH);
 analogWrite(PWM_A, 255); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delayMicroseconds(delayMs);
 
 
    //digitalWrite(DIR_B, HIGH);
 analogWrite(PWM_A, 255); // Ch. A off
 analogWrite(PWM_B, 0); // Ch. B on
 delayMicroseconds(delayMs);
 
 
// digitalWrite(DIR_A,LOW); // Ch. A forward
 digitalWrite(DIR_B, LOW); // Ch. B forward
 analogWrite(PWM_A, 255); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delayMicroseconds(delayMs);
 
 
//  digitalWrite(DIR_A,LOW); // Ch. A forward
 //digitalWrite(DIR_B, LOW); // Ch. B forward
 analogWrite(PWM_A, 0); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delayMicroseconds(delayMs);
 
  digitalWrite(DIR_A,HIGH); // Ch. A forward
 //digitalWrite(DIR_B, LOW); // Ch. B forward
 analogWrite(PWM_A, 255); // Ch. A off
 analogWrite(PWM_B, 255); // Ch. B on
 delayMicroseconds(delayMs);
}


## Robot Arm:

### Step 1 : URDF:
<?xml version="1.0"?>
<robot name="roco_arm">

  <material name="blue">
   <color rgba="0 0 0.8 1"/>
  </material>

  <material name="white">
    <color rgba="1 1 1 1"/>
  </material>

  <material name="green">
    <color rgba="0 0.8 0 1"/>
  </material>


  <link name="base_link">
    <visual>
      <geometry>
      <cylinder length="0.05" radius="0.08"/>
      </geometry>
      <material name="white"/>
    </visual>
  </link>


  <link name="first_segment">
    <visual>
      <geometry>
      <box size="0.1 0.1 0.1"/>
      </geometry>
      <material name="blue"/>
    <origin rpy="0 0 0" xyz="0 0 0" />
    </visual>
  </link>



   <link name="second_segment">
    <visual>
      <geometry>
      <box size="0.15 0.02 0.03"/>
      </geometry>
     <origin rpy="0 0 0" xyz="-0.09 0 0" />
    </visual>
  </link>



  <link name="third_segment">
    <visual>
      <geometry>
      <box size="0.10 0.02 0.03"/>
      </geometry>
      <material name="green"/>
     <origin rpy="0 0 0" xyz="-0.065 0 0" />
    </visual>
  </link>

 

  

  <joint name="base_to_first" type="revolute">
    <axis xyz="0 0 -1" />
    <limit effort="1000" lower="0" upper="3.14" velocity="0.5" />
    <parent link="base_link"/>
    <child link="first_segment"/>
    <origin xyz="0 0 0.03" />
  </joint>

 
 <joint name="first_to_second" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="0" upper="3.14" velocity="0.5" />
    <parent link="first_segment"/>
    <child link="second_segment"/>
    <origin xyz="0 0 0.035" />
    
  </joint>

 



  <joint name="second_to_third" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="-1.5" upper="1.5" velocity="0.5" />
    <parent link="second_segment"/>
    <child link="third_segment"/>
   <origin xyz="-0.15 0 0" />
  </joint>


</robot>

### Step 2: Arduino Code:
include <Servo.h>
include <ros.h>
include <sensor_msgs/JointState.h>

using namespace ros;

NodeHandle nh;
Servo servo0;
Servo servo1;
Servo servo2;

void cb( const sensor_msgs::JointState& msg){
int angle0 = (int) (msg.position[0] * 180/3.14);
int angle1 = (int) (msg.position[1] * 180/3.14);
int angle2 = (int) (msg.position[2] * 180/3.14);
servo0.write(angle0); // 0-180
servo1.write(angle1); // 0-180
servo2.write(angle2); // 0-180
}



Subscriber<sensor_msgs::JointState>
sub("joint_states", cb);

void setup(){
nh.initNode();
nh.subscribe(sub);

servo0.attach(9); //attach it to pin 9
servo1.attach(10);
servo2.attach(11);
}

void loop(){
nh.spinOnce();
delay(1);
}

### Step 3: RVIZ:

[RVIZ simulation](https://photos.app.goo.gl/m384chBEFksHYJGk1)

### Step 4: Final Product:
[Arm FInished](https://photos.app.goo.gl/N2K8QtcsK3VqRQyu2)

+ Improvements:
 - our original intention was to add a fourth degree of movement controlling a claw at the end of the arm, however due to the glue not holding on the screw (weakening the movement of the other parts) this was not possible as the weight would have caused the arm to topple. 
- the glue used was not very effective, so tape had to be used which did not look as aesthetically pleasing as originally planned.









