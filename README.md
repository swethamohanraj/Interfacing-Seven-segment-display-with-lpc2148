# Interfacing-Seven-segment-display-with-lpc2148
```
Name:K.M.Swetha	
Roll no:21221240055
Date of experiment:16.11.2022



Ex. No 08:Interfacing-Seven-segment-display-with-lpc2148
 
``` 

### Aim: To configure and display 4 character LED seven segment display and write a c code for displaying number 1 to 9 and A to F 
### Components required: Proteus ISIS professional suite, Kiel μ vision 5 Development environment 
 ![image](https://user-images.githubusercontent.com/36288975/201021692-efa39349-1a3c-4737-aadc-1843b954c78d.png)
Figure-01 Internal circuit for seven segment MPX4 display



### Theory: 
	7 Segment Display has seven segments in it and each segment has one LED inside it to display the numbers by lighting up the corresponding segments. Like if you want the 7-segment to display the number "5" then you need to glow segment a,f,g,c, and d by making their corresponding pins high. There are two types of 7-segment displays: Common Cathode and Common Anode, here we are using Common Cathode seven segment display.
   ![image](https://user-images.githubusercontent.com/36288975/201021740-565b47cd-26d8-4e54-a092-eef7a0a85278.png)
 
          Figure-02 Pin configuration for seven segment display  


Below table shows the HEX values and corresponding digit according to LPC2148 pins for common cathode configuration.



Sl no 	Hex code 	Output of LCD
1	0x88	1
2	0xeb	2
3	0x4c	3
4	0x49	4
5	0x2b	5
6	0x19	6
7	0x18	7
8	0xcb	8
9	0x8	9
10	0x9	A
11	0xa	B
12	0x38	C
13	0x9c	D
14	0x68	E
15	0x1c 	F
16	0x1e	0

 

![image](https://user-images.githubusercontent.com/36288975/201021930-7efe2b15-b0de-4d52-b87d-329fe6b91c89.png)
        Figure -3 Circuit diagram of interfacing for LPX4 - CA

## Kiel - Program 
```
#include <LPC214x.H>
unsigned char dig[]= {0x88,0xeb,0x4c,0x49,0x2b,0x19,0x18,0xcb,0x8,0x9,0xa,0x38,0x9c,0x68,0x1c,0x1e};

void delay(unsigned int count)
{
	int j=0,i=0;
	for(j=0;j<count;j++)
	{
		for(i=0;i<120;i++);
	}
}

int main(void)
{
	unsigned char count=0;
	unsigned int i=0;
	IO0DIR |= (1 << 11);
	IO0SET |= (1 << 11);
	IO0DIR |= 0x007F8000;
	while(1)
	{
		count++;
		if(count == 16)count=0;
		for(i=0;i<800;i++)
		{
			IO0CLR = 0x007f8000;
			IO0SET = (dig[count] << 15);
			delay(200);
		}
  }
}
```

### Output:
## Before Stimulation:
![swethbef](https://user-images.githubusercontent.com/94228215/202232571-13abf862-a4dd-43cd-9fcb-a9c0127804e0.png)

## After Stimulation(Digit):
![swethaf1](https://user-images.githubusercontent.com/94228215/202232637-52972b05-087e-4f0f-b2cd-e2ed4e271722.png)

## After Stimulation(Alphabet):
![swethaf2](https://user-images.githubusercontent.com/94228215/202232799-2f85dbb9-e138-4ef4-ad29-efc84d806744.png)

## Circuit Diagram:
![swethpdf](https://user-images.githubusercontent.com/94228215/202232846-20cd9b96-8499-4ffe-a5df-4cd92d94d104.png)

### Result :
LED seven segment display is interfaced and displayed alpha numeric characters 


