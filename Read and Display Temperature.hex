#include <REGX51.H>
//Khai bao chan giao tiep ADC0809
#define ADC0809_DATA 		P3	
#define ADC0809_A  		P2_0 
#define ADC0809_B  		P2_1
#define ADC0809_C  		P2_2
#define ADC0809_ALE   		P2_3
#define ADC0809_START  	P2_4
#define ADC0809_EOC   		P2_5
#define ADC0809_OE   		P2_6
#define ADC0809_CLK		P2_7


//Khai bao chan giao tiep LCD16x2 4bit
#define LCD_RS 		P0_0
#define LCD_RW 		P0_1
#define LCD_EN	 	P0_2
#define LCD_D4 		P0_4
#define LCD_D5 		P0_5
#define LCD_D6 		P0_6
#define LCD_D7 		P0_7


/*****************ADC0809*********************/
//Ham doc ADC0809 theo kenh
unsigned char ADC0809_Read(unsigned char channel){
	unsigned char kq;
 	ADC0809_A = channel & 0x01;
	ADC0809_B = channel & 0x02;
	ADC0809_C = channel & 0x04;
	ADC0809_ALE 	= 1;
	ADC0809_START = 1;
	ADC0809_ALE 	= 0;
	ADC0809_START = 0;
	while(ADC0809_EOC);
	while(!ADC0809_EOC);
	ADC0809_OE = 1;
	kq = ADC0809_DATA;
	ADC0809_OE = 0;
	return kq;
}


/*****************Ham delay bằng Timer*********************/
void delay(unsigned int count, unsigned int timer)
{ unsigned char i;
for(i=0;i<count;i++)
{TH1=-timer/256;
TL1=-timer%256;
TR1=1;
while(!TF1);
TR1=TF1=0;
}
}

/**************Ctr giao tiep LCD 16x2 4bit**********************/
void LCD_Enable(void){
        LCD_EN =1;
        delay(50,10000);
        LCD_EN=0;}


//Ham Gui 4 Bit Du Lieu Ra LCD
void LCD_Gui4Bit(unsigned char Data){
        LCD_D4=Data & 0x01;
        LCD_D5=(Data>>1)&1;
        LCD_D6=(Data>>2)&1;
        LCD_D7=(Data>>3)&1;
}


// Ham Gui 1 Lenh Cho LCD
void LCD_ghi_lenh(unsigned char command){
        LCD_Gui4Bit(command >>4);	/* Gui 4 bit cao */
        LCD_Enable();
        LCD_Gui4Bit(command); 	/* Gui 4 bit thap*/
        LCD_Enable();
}
void LCD_xoa(){// Ham Xoa Man Hinh LCD
        LCD_ghi_lenh(0x01); 
        delay(20,10000);
}
// Ham Khoi Tao LCD
void LCD_Init(){
        LCD_Gui4Bit(0x00);
        delay(50,10000);
        LCD_RS=0;
        LCD_RW=0;
        LCD_Gui4Bit(0x03);
        LCD_Enable();
        delay(50,10000)
        LCD_Gui4Bit(0x02);
        LCD_Enable();
        LCD_ghi_lenh( 0x28 );	 // giao thuc 4 bit, hien thi 2 hang, ki tu 5x8
        LCD_ghi_lenh( 0x0c); 	// cho phep hien thi man hinh
        LCD_ghi_lenh( 0x06 ); 	// tang ID, khong dich khung hinh
        LCD_ghi_lenh(0x01); 	// xoa toan bo khung hinh
}
void LCD_DieuKhien(unsigned char x, unsigned char y){
        unsigned char address;
        if(!y)address=(0x80+x);
        else address=(0xc0+x);
        LCD_ghi_lenh(address);
        delay(50,10000);
}
void LCD_gui_kitu(unsigned char Data){	//Ham Gui 1 Ki Tu
        LCD_RS=1;
        LCD_ghi_lenh(Data);
        LCD_RS=0 ;
}
void LCD_chuoi(char *s){			//Ham gui 1 chuoi ky tu
        while (*s){
                LCD_gui_kitu(*s);
                s++;
        }
}


//************** Hàm tính toán nhiệt độ ***********************
unsigned char Temp(unsigned char adc) 	
{	
	 return (adc); 				
	 
}  
void TempShow(unsigned char z){		 
     LCD_chuoi("Nhiet do: ");
     LCD_gui_kitu((z/100)+48);			
     LCD_gui_kitu((z%100/10)+48);		
     LCD_gui_kitu(((z%100)%10)+48); 
     LCD_chuoi("'C");
}


/******************Ctr ngat timer 0**************************/
void INT_Timer0()interrupt 1	 //ctr phuc vu ngat tao xung clock cho ADC0809
{
     ADC0809_CLK=~ADC0809_CLK;	 //Dao bit
}


/******************Ctr chinh**************************/
unsigned char temp;
void main(){
	unsigned char max = 65;
	P0=0 ;
	//Tao xung clock cho ADC0809 dung ngat timer
	TMOD=0x02; 	//Timer0 8bit tu nap lai
	TH0=TL0=236;	//Tao ngat 20us
	TR0=1;		//Khoi dong timer0
   	ET0=1;			//Ngat timer0
    	EA=1;			//Cho phep ngat cuc bộ	
	LCD_Init();		//Khoi tao LCD
    	delay(50,10000);
	LCD_chuoi("Do nhiet do...");//Gui chuoi len LCD
   	 delay(50,10000);
    	LCD_xoa();		//Xoa man hinh
	LCD_DieuKhien(0,1);
	LCD_chuoi("T.Nha - V.Hung");
	while(1){
	
		  LCD_DieuKhien(0,0);
		  temp=ADC0809_Read(0); //Doc ADC0
		  temp=Temp(temp);	 //Tinh nhiet do
		  TempShow(temp); 	//Hien thi nhiet do
		  delay(50,10000);		//0.5s doc mot lan	
	}
}
