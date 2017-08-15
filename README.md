# 2017-2018-FTC-Robotics-Code-Fortissimus
This is the beginning of a new era for CHS Robotics!!!

TeleOp 3

package org.firstinspires.ftc.teamcodeFort;

import com.qualcomm.robotcore.eventloop.opmode.OpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.Servo;

/**
* Created by robotics on 10/5/2016.
*/
@TeleOp(name="TankDriveTeleOp3")
public class TankDriveTeleOp3 extends OpMode {
   DcMotor leftMotor;
   DcMotor rightMotor;
   DcMotor reelMotorr;
   DcMotor reelMotorl;
   Servo armleft = null;
   Servo armright = null;
   Servo brake = null;
   Servo shoot = null;

   @Override
   public void init() {

       leftMotor = hardwareMap.dcMotor.get("left_drive");
       armleft = hardwareMap.servo.get("armleft");
       armright = hardwareMap.servo.get("armright");
       brake = hardwareMap.servo.get("brake");
       shoot = hardwareMap.servo.get("shoot");
       rightMotor = hardwareMap.dcMotor.get("right_drive");
       reelMotorr = hardwareMap.dcMotor.get("reel_driver");
       reelMotorl = hardwareMap.dcMotor.get("reel_drivel");
       leftMotor.setDirection(DcMotor.Direction.REVERSE);

       armleft.setPosition(.7);
       armright.setPosition(0);
       shoot.setPosition(.5);
       brake.setPosition(.5);

   }

   @Override
   public void loop() {
       float leftY = gamepad1.left_stick_y;
       float rightY = gamepad1.right_stick_y;
       float right_trigger = gamepad2.right_trigger;
       float left_trigger = gamepad2.left_trigger;

       boolean mode;
       int timer;
       if (gamepad1.dpad_down||gamepad1.dpad_up||gamepad1.dpad_left||gamepad1.dpad_right){
           if (gamepad1.dpad_up){
               leftMotor.setPower(.2);
               rightMotor.setPower(.2);
           }
           if (gamepad1.dpad_down){
               leftMotor.setPower(-.2);
               rightMotor.setPower(-.2);
           }
           if (gamepad1.dpad_left){
               leftMotor.setPower(-.2);
               rightMotor.setPower(.2);
           }
           if (gamepad1.dpad_right){
               leftMotor.setPower(.2);
               rightMotor.setPower(-.2);
           }
       } else {
           if (leftY > .1 || leftY < -.1) {
               leftMotor.setPower(.6*leftY);
           } else {
               leftMotor.setPower(0);
           }
           if (rightY > .1 || rightY < -.1) {
               rightMotor.setPower(.6*rightY);
           } else {
               rightMotor.setPower(0);
           }
       }
       if (gamepad2.dpad_down) {
           brake.setPosition(-.4);
       }
       else if (gamepad2.dpad_up) {
           brake.setPosition(.4);
       }
       if (gamepad2.x) {
           armleft.setPosition(.7);
       }
       else if (gamepad2.b) {
           armleft.setPosition(.05
           );
       }
       if (gamepad2.y) {
           armright.setPosition(-.1);
       }
       else if (gamepad2.a) {
           armright.setPosition(-.9);
       }
       /*if (y = true){
           if (timer >= 100) {
               if (mode = true){
                   mode = false;
                   timer = 0;
               } else{
                   mode = true;
                   timer = 0;
               }

           }
       }
       if (right_trigger > .1 || left_trigger > .1) {
           if (right_trigger > .1) {
               reelMotorr.setPower(right_trigger);
               reelMotorl.setPower(right_trigger);
           }
           if (left_trigger > .1) {
               reelMotorr.setPower(-left_trigger);
               reelMotorl.setPower(-left_trigger);
           }
       } else {
           reelMotorr.setPower(0);
           reelMotorl.setPower(0);
       }*/
       double Ileft_trigger=left_trigger+.1;
       if (right_trigger >= Ileft_trigger){
           reelMotorl.setPower(-.2);
       }
       reelMotorl.setPower(-right_trigger + left_trigger);
   }
}
