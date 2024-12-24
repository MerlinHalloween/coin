# coin

https://youtu.be/atA9PljkhF8

this video shows the gaming demonstration
the four bit button got (left)(right)(restart)(pause),four different state

when pass,show V on 8x8 matrix led;
else if, show X on matrix,and the beeper will generate a long beep sound

you can restart the game by pressing restart

new function added:
beeper
pause
restart
different dificulty choice for 0.5X,1X,2X,4X(even 16X:in the code//)



PS: i add extra lose state expression which is 
LO
SE
in the drop_19 parameter
the matrix coding should base on the rule:73516240
when you write on the parameter,refer to my note pic:16995


Base on the origin project, the count down system is base on 16 bit led,but i got only 8 pin to assign .
Due to that case,i change the count down system as the 8 bit led light will -1 to snub out all 8 bit,then the phase will change to 1,and the 8 bit led will +1 light up again .Hence,one loop represent the gaming time.

if you wanna change the X color,change drop_19, assign it to B,and let R G<=8'b11111111.

more explanation about the basic function of normal coin game should have,refer to the link below.





reference:
https://github.com/joe0411/final-1
