const int HS1101_Table[101]=
                        {
                         7410,7392,7374,7357,7340,7323,7307,7290,7274,7259,
                         7243,7228,7213,7198,7183,7169,7155,7140,7127,7113,
                         7099,7086,7072,7059,7046,7033,7020,7007,6995,6982,
                         6969,6957,6945,6932,6920,6908,6896,6884,6872,6860,
                         6848,6836,6824,6812,6800,6788,6776,6764,6752,6740,
                         6728,6716,6704,6692,6680,6668,6656,6643,6631,6619,
                         6606,6594,6581,6568,6556,6543,6530,6517,6504,6491,
                         6477,6464,6450,6437,6423,6409,6395,6381,6367,6352,
                         6338,6323,6309,6294,6279,6264,6248,6233,6217,6202,
                         6186,6170,6154,6137,6121,6104,6087,6070,6053,6036,
                         6019
                        } ;
unsigned int docdoam(unsigned int tanso)
  {
  unsigned int i;
for(i=0;i<101;i++)    {  if ((tanso+25)>bangtanso[i])  return i;}
 return 100;
}
void hienthidoam(unsigned char z){ //Chuyen doi hien thi
     LCD_chuoi ("Do Am : ");
     LCD_gui_kitu ((z/100)+0x30);//Tram
     LCD_gui_kitu ((z%100/10)+0x30);//Chuc
     LCD_gui_kitu ((z%10)+0x30);//Don vi 
     LCD_chuoi("%");
}
void main()
{
unsigned int t, tanso,doam;
TMOD &= 0xf0;
TMOD |= 0x09;// GATE=1, MODE 1 CUA TIMER 0
while(1)
{
TH0=TL0=0;
while(INT0);  // doi het muc 1 cua xung
while(!INT0); // doi het muc 0 cua xung
TR0=1;
while(INT0);
TR0=0;
t=TH0;	
t <<= 8;
t |= TL0;
t=t*2;
tanso=1000000/t;
doam= docdoam(tanso);
LCD_chuoi("Test Do Am");
hienthidoam(doam);
	}
