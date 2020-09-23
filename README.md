<div align="center">

## Neuters  Dictionary


</div>

### Description

Working same as a Dictionary.

Add words , meanings and than you can save it for future purposes.
 
### More Info
 
not any

self explainatory stuff.

Add words , meanings and than you can save it for future purposes.

not at all


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Syed  Umair  Ali  Shah](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/syed-umair-ali-shah.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__3-2.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/syed-umair-ali-shah-neuters-dictionary__3-2524/archive/master.zip)

### API Declarations

```
#include <fstream.h>
#include <string.h>
#include <conio.h>
#include <stdio.h>
#include <iostream.h>
#include <graphics.h>
#include <dos.h>
```


### Source Code

```
/////////////////////////////////////////////////////////////////////////////
/*
	IN THE NAME OF ALLAH THE MOST MERCIFUL THE MOST GRACOIUS
*/
/////////////////////////////////////////////////////////////////////////////
/*
			GROUP # 01 PRESENTS
			NEUTERS DICTIONARY
*/
/////////////////////////////////////////////////////////////////////////////
			/* HEADER FILES */
/////////////////////////////////////////////////////////////////////////////
#include <fstream.h>
#include <string.h>
#include <conio.h>
#include <stdio.h>
#include <iostream.h>
#include <graphics.h>
#include <dos.h>
////////////////////////////////////////////////////////////////////////////
		   /* GLOBALLY DEFINED ELEMENTS */
///////////////////////////////////////////////////////////////////////////
const int max=40;
enum found {true,false};
found word_found;
long n;
fstream temp_file;
fstream dic_file;
///////////////////////////////////////////////////////////////////////////
			/* CLASS DECLARATION */
//////////////////////////////////////////////////////////////////////////
class dictionary
{
	public:
		void add_new_word(char *w_ord,char *m_eaning);
		void show_meaning(char *w_ord);
		void delete_a_word(char *w_ord);
		void save_in_file();
		void read_from_file(int file_pos);
		long size_of_file();
	private:
		char word[max],meaning[max];
};
////////////////////////////////////////////////////////////////////////////
			/* ADD FUNCTION*/
///////////////////////////////////////////////////////////////////////////
void dictionary::add_new_word(char *w_ord,char *m_eaning)
  {
   strcpy(dictionary::word,w_ord);
   strcpy(dictionary::meaning,m_eaning);
  };
////////////////////////////////////////////////////////////////////////////
			/* MEANING FUNCTION*/
////////////////////////////////////////////////////////////////////////////
void dictionary::show_meaning(char *w_ord)
  {
   if (strcmp(word,w_ord)==0)
    {
	word_found=true;
	gotoxy(10,17);
	cprintf("MEANING OF ");cprintf(w_ord);cprintf(" is ");cout<<endl;
	gotoxy(10,18);
	cprintf("      ");cprintf(meaning);cout<<endl;
	getch();
    };
  };
/////////////////////////////////////////////////////////////////////////////
		   /* DELETE A WORD FUNCTION */
/////////////////////////////////////////////////////////////////////////////
void dictionary::delete_a_word(char *w_ord)
  {
  if (strcmp(word,w_ord)==0)
    {
	word_found=true;
    };
  };
/////////////////////////////////////////////////////////////////////////////
		    /* SAVE IN FILE FUNCTION */
/////////////////////////////////////////////////////////////////////////////
void dictionary::save_in_file()
  {
   dic_file.write((char*)this,sizeof(*this));
  };
/////////////////////////////////////////////////////////////////////////////
			/* READ FROM FILE FUNCTION */
/////////////////////////////////////////////////////////////////////////////
void dictionary::read_from_file(int file_pos)
  {
   dic_file.seekg(file_pos*sizeof(dictionary));
   dic_file.read((char*)this,sizeof(*this));
  };
/////////////////////////////////////////////////////////////////////////////
			/*SIZE OF FILE FUNCTION*/
/////////////////////////////////////////////////////////////////////////////
long dictionary::size_of_file()
  {
   dic_file.seekg(0,ios::end);
   return dic_file.tellg()/sizeof(dictionary);
  };
////////////////////////////////////////////////////////////////////////////
			/* WHERE GRAPHICS HAS TO PLAY */
////////////////////////////////////////////////////////////////////////////
void start(void);
void end(void);
/////////////////////////////////////////////////////////////////////////////
			/* START OF MAIN */
/////////////////////////////////////////////////////////////////////////////
void main()
	{
	char choice;
	dictionary dict;
	char w_ord[max];
	char m_eaning[max];
	start();
do
	{
	clrscr();
	temp_file.open("temp.dic",ios::app|ios::binary|ios::in|ios::out);
	dic_file.open("data.dic",ios::app|ios::binary|ios::in|ios::out);
	textcolor(2);
gotoxy(10,9);
cprintf("----------------PLEASE GO,AHEAD----------------\n");
gotoxy(10,10);
		cprintf("YOU HAVE THE FOLLOWING CHOICES\n");
gotoxy(10,11);
		cprintf("1: ADD WORD\n");
gotoxy(10,12);
		cprintf("2: GET MEANING\n");
gotoxy(10,13);
		cprintf("3: DELETE A WORD\n");
gotoxy(10,14);
		cprintf("4: EXIT\n");
gotoxy(10,15);
		choice=getch();
////////////////////////////////////////////////////////////////////////////
switch(choice)
		  {
////////////////////////////////////////////////////////////////////////////
			/* CASE # 01 */
////////////////////////////////////////////////////////////////////////////
	  case '1':
		  {
		  gotoxy(10,15);
		   cprintf("ENTER WORD TO ADD AND ITS MEANING\n" );
		   gotoxy(10,16);
		   cin>>w_ord;
		   cin.ignore(1,'\n');
		   gotoxy(10,17);
		   cin.get(m_eaning,max,'\n');
		   dict.add_new_word(w_ord,m_eaning);
		   dict.save_in_file();
		   dic_file.close();
		   temp_file.close();
		   gotoxy(10,18);
		   cprintf("WORD ADDED SUCCESSFULLY");cout<<endl;
		   getch();
		   };
		   break;
////////////////////////////////////////////////////////////////////////////
			/*CASE # 02*/
///////////////////////////////////////////////////////////////////////////
case '2':
	  {
		   gotoxy(10,15);
		   cprintf("ENTER WORD TO GET MEANING\n");
		   gotoxy(10,16);
		   cin>>w_ord;
		   word_found=false;
		   int j=0;
		   n =dict.size_of_file();
while((j<n)&&(word_found))
			  {
			  dict.read_from_file(j);
			  dict.show_meaning(w_ord);
			  j++;
			  };
if (word_found==false)
			  {
			  gotoxy(10,17);
			  cprintf("NO SUCH WORD IN DICTIONARY");
			  getch();
			  }
dic_file.close();
temp_file.close();
		   };
		   break;
/////////////////////////////////////////////////////////////////////////////
			/*CASE # 03*/
/////////////////////////////////////////////////////////////////////////////
case '3':
	  {
		   gotoxy(10,15);
		   cprintf("ENETER WORD TO GET DELETE\n");
		   gotoxy(10,16);
		   cin>>w_ord;
		   word_found=false;
		   int j=0;
		   n =dict.size_of_file();
		   dict.read_from_file(j);
		   j++;
		   dict.delete_a_word(w_ord);
while((j<n)&&(word_found))
			  {
			  temp_file.write((char*)&dict,sizeof(dict));
			  dict.read_from_file(j);
			  dict.delete_a_word(w_ord);
			  j++;
			  };
while(j<n)
			  {
			  dict.read_from_file(j);
			  temp_file.write((char*)&dict,sizeof(dict));
			  j++;
			  };
			  if(word_found==false)
			  {
			  temp_file.write((char*)&dict,sizeof(dict));
			  gotoxy(10,17);
			  cprintf("NO SUCH WORD IN DICTIONARY");cout<<endl;
			  gotoxy(10,18);
			  cprintf("DELETE OPERATION CANNOT BE PERFORMED");
			  getch();
			  }
else
			  {
			  gotoxy(10,17);
			  cprintf("DELETION OPERATION WAS SUCESSFULL");
			  cout<<endl;
			  getch();
			  }
dic_file.close();
temp_file.close();
		   remove("data.dic");
		   rename("temp.dic","data.dic");
};
break;
default:
	   {
		   dic_file.close();
		   temp_file.close();
	   }
	  }; //end of switch
   }
   while (choice!='4'); //end of do loop
   end();
  }; //end of main
////////////////////////////////////////////////////////////////////////////
			/* GRAPHICS DECLARATION */
/////////////////////////////////////////////////////////////////////////////
void start(void)
		{
		int gdriver = DETECT, gmode, errorcode;
		int style, midx, midy;
		initgraph(&gdriver, &gmode, "c:\\tc\\bgi");
		errorcode = graphresult();
if (errorcode != grOk)
		{
		printf("Graphics error: %s\n", grapherrormsg(errorcode));
		printf("Press any key to halt:");
		getch();
		}
  midx = getmaxx() / 2;
bar(50,70,600,150);
		for (int i=0;i<10;i++)
		{
		settextjustify(CENTER_TEXT, CENTER_TEXT);
		setbkcolor(BLACK);
		bar3d(50,70,600,150,10,1);
		setfillstyle(SOLID_FILL,BLUE);
		settextstyle(SANS_SERIF_FONT, HORIZ_DIR, 0);
		moveto(midx, 100);
		setusercharsize(i+1,6, i+1, 6);
		outtext(" NEUTERS DICTIONARY");
		sound(500);
		delay(250);
		nosound();
		settextstyle(SANS_SERIF_FONT, HORIZ_DIR,0);
		}
setcolor(9);
settextstyle(TRIPLEX_FONT,HORIZ_DIR, 3);
		for (int k=300;k>=60;k--)
		{
		setcolor(WHITE);
		outtextxy(midx-k,200,"A");
		delay(40);
		setcolor(BLACK);
		outtextxy(midx-k,200,"A");
		k=k-10;
		}
for (int n=300;n>=20;n--)
		{
		setcolor(WHITE);
		outtextxy(midx-75,200,"A");
		outtextxy(midx-8,200+n,"PROJECT");
		delay(40);
		setcolor(BLACK);
		outtextxy(midx-8,200+n,"PROJECT");
		n=n-10;
		}
for (int o=300;o>=60;o--)
		{
		setcolor(WHITE);
		outtextxy(midx-8,200,"PROJECT");
		outtextxy(midx+o+50,200,"BY");
		delay(40);
		setcolor(BLACK);
		outtextxy(midx+o+50,200,"BY");
		o=o-10;
		}
		setcolor(WHITE);
		settextstyle(TRIPLEX_FONT,HORIZ_DIR, 3);
		outtextxy(midx,200,"A PROJECT BY");
		delay(300);
		setcolor(WHITE);
		settextstyle(DEFAULT_FONT,HORIZ_DIR, 2);
		outtextxy(midx,250,"GROUP # 01");
		setcolor(9);
		rectangle(185,300,440,425);
		setcolor(WHITE);
		settextstyle(SANS_SERIF_FONT,HORIZ_DIR, 2);
		outtextxy(midx,320,"Syed Umair Ali Shah");
		outtextxy(midx,340,"       ");
		settextstyle(SANS_SERIF_FONT,HORIZ_DIR, 2);
		outtextxy(midx,360,"NAAZIA AFZAAL");
		outtextxy(midx,380,"      ");
		settextstyle(TRIPLEX_FONT, HORIZ_DIR, 2);
		setcolor(BLUE);
		outtextxy(midx+150,450,"PRESS ANY KEY TO CONTINUE...");
		getch();
		closegraph();
		}
		void end(void)
		{
		int gdriver = DETECT, gmode, errorcode;
		initgraph(&gdriver, &gmode, "c:\\tc\\bgi");
		errorcode = graphresult();
		if (errorcode != grOk)
		{
		printf("Graphics error: %s\n", grapherrormsg(errorcode));
		printf("Press any key to halt:");
		getch();
		}
		setbkcolor(BLACK);
		settextstyle(TRIPLEX_FONT, HORIZ_DIR, 4);
		moveto(5, getmaxy() / 2.5);
		setusercharsize(2, 1, 1, 1);
		outtext("THANKS FOR USING");
		moveto(190,250);
		outtext("MY PROGRAM");
		getch();
		closegraph();
		}
////////////////////////////////////////////////////////////////////////////
				/* THE END*/
/////////////////////////////////////////////////////////////////////////////
```

