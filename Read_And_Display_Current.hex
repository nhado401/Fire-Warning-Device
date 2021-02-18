Void CurrentShow (void)
//hàm đọc ADC đã viết rồi nên tận dụng.
for (i=0;i<=1000;i++)
{  ADC=ADC0809_Read(1);	
      if (i<1000)
       {
            tong=tong+ADC;			//Lấy mẫu.
            i++;
       }
       else
       {     
            tong=tong/1000;
            dong = (int) (tong-128+1)/0.5632*1000
	CurrentShow(dong);tong=0; i=0;  
  }
}
void CurrentShow(unsigned char z)
{
     LCD_chuoi("Dong dien:");     //Hàm gởi kí tự đã có rồi nên tận dụng.
     LCD_gui_kitu((z/1000)+48);			//Nghìn
     LCD_gui_kitu((z%1000/100)+48);			//Tram
     LCD_gui_kitu((((z%1000)%100)/10)+48);		//Chuc
     LCD_gui_kitu((((z%1000)%100)%10)+48);		//Đơn vị
     LCD_chuoi("mA");
}
