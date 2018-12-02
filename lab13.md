##贪吃蛇实验报告  
#程序思路：  
1）用H表示蛇的头，用X表示蛇身，$表示食物，蛇每吃掉一个$就会加一个X，用*表示边界，当H“接触”到X或边界的时候，game over。  
2）<move>函数：当输入w,a,s,d时，蛇就会向上，左，右，下移动一步，提前判断下一步上是否为H或X或*或$，当接触到$时，调用<eat>函数。  
3）<eat>函数：蛇吃掉$后，在蛇的最后面加上一个X，注意排除*以及其它X。  
4)移动思想：H移动后，X的坐标依次替换为前一个H或X的坐标，将尾部的X变为空格，即可实现蛇的移动。  
5）图像显示：先输入一个外部二维数组char map[][]，初始化为游戏界面，此后通过改变数组部分坐标的元素后，再次输出map的方法实现游戏。  
#程序：
#include<stdio.h>  

//#include<stdlib.h>  

int X[100]={1},Y[100]={1},game_over=1,j=0;  

int s[]={1,3,7,2,4,1,6,7,9,8,1,5,7,3,10,9,4,2,3,5,9,5,1,6,3,2,5,4,2,3,10,1,3,2,2,5,10,6,7,9,8,1,5,10,8,10,9,4,2,3,5,9,5,1,6,3,2,5,4,2,3,10,  

1,3,7,3,4,10,6,7,9,8,4,5,7,3,10,9,4,2,3,5,9,5,1,6,3,2,5,4,2,3,10,1,3,7,7,4,10,6,7,9,8,1,5,7,3,10,9,4,2,3,5,9,5,1,6,3,5,5,4,2,3,10};  

char map_1[][13]={  

	"************",  

	"*          *",  

	"*          *",  

	"*  Game    *",  

	"*    Over  *",  

	"*      !!! *",  

	"*          *",  

	"*          *",  

	"*          *",  

	"*          *",  

	"*          *",  

	"************"};                  //游戏结束图像  

int rand_map(char map[][13]){  

	int t=0;  

	int yer=1;  

	while(yer){  

	if(map[s[j+t]][s[j+t+1]]!='H'&&map[s[j+t]][s[j+t+1]]!='X'){  

			map[s[j+t]][s[j+t+1]]='$';--yer;}  

	else ++t;  

	}  

}  

void print_map(char s[][13]){  

	for(int i=0;i<12;++i)  

	printf("%s\n",s[i]);  

}  


void eat(char map[][13]){
		if(map[Y[j]-1][X[j]]!='*'&&map[Y[j]-1][X[j]]!='X'&&map[Y[j]-1][X[j]]!='H'&&map[Y[j]-1][X[j]]!='$'){
			map[Y[j]-1][X[j]]='X';
			Y[j+1]=Y[j]-1;
			X[j+1]=X[j];
		}
		else if(map[Y[j]][X[j]-1]!='*'&&map[Y[j]][X[j]-1]!='X'&&map[Y[j]][X[j]-1]!='H'&&map[Y[j]][X[j]-1]!='&'){
			map[Y[j]][X[j]-1]='X';
			Y[j+1]=Y[j];
			X[j+1]=X[j]-1;
		}
		else if(map[Y[j]+1][X[j]]!='*'&&map[Y[j]+1][X[j]]!='X'&&map[Y[j]+1][X[j]]!='H'&&map[Y[j]+1][X[j]]!='$'){
			map[Y[j]+1][X[j]]='X';
			Y[j+1]=Y[j]+1;
			X[j+1]=X[j];
		}
		else{
			map[Y[j]][X[j]+1]='X';
			Y[j+1]=Y[j];
			X[j+1]=X[j]+1;
		}
		++j;
}
void move(char map[][13]){
	char m=getchar();
	switch(m){
		case 'a':{
			int bl=0;
			if(X[0]-1==0||map[Y[0]][X[0]-1]=='X'){
				game_over--;
				return;
			}
			else{
				if(map[Y[0]][X[0]-1]=='$'){eat(map);bl++;}   //吃吃吃 
				
				map[Y[j]][X[j]]=' ';
				if(j!=0){
				map[Y[0]][X[0]]='X';
				for(int i=j;i>0;--i){
					Y[i]=Y[i-1];
					X[i]=X[i-1];
					}
				}    								//坐标挪位 
				
				map[Y[0]][--X[0]]='H';
				if(bl) rand_map(map);
				print_map(map);
			}
			break;
		}
		case 'd':{
			int bl=0;
			if(X[0]+1==11||map[Y[0]][X[0]+1]=='X'){
				game_over--;
				return;
			}
			else{
				if(map[Y[0]][X[0]+1]=='$'){
					eat(map);
					++bl;
				}   //吃吃吃
				 
				map[Y[j]][X[j]]=' ';
				if(j!=0){
				map[Y[0]][X[0]]='X';
				for(int i=j;i>0;--i){
					Y[i]=Y[i-1];
					X[i]=X[i-1];
					}
				}    								//坐标挪位 
				
				map[Y[0]][++X[0]]='H';
				if(bl) rand_map(map);
				print_map(map);
			}
			break;
		}
		case 'w':{
			int bl=0;
				if(Y[0]-1==0||map[Y[0]-1][X[0]]=='X'){
				game_over--;
				return;
			}
			else{
				if(map[Y[0]-1][X[0]]=='$'){
					eat(map);
					++bl;
				} //吃吃吃 
				
				map[Y[j]][X[j]]=' ';
				if(j!=0){
				map[Y[0]][X[0]]='X';
				for(int i=j;i>0;--i){
					Y[i]=Y[i-1];
					X[i]=X[i-1];
					}
				}    								//坐标挪位 
				
				map[--Y[0]][X[0]]='H';
				if(bl) rand_map(map);
				print_map(map);
			}
			break;
		}
		case 's':{
			int bl=0;
			if(Y[0]+1==11||map[Y[0]+1][X[0]]=='X'){
			game_over--;
			return;
			}
			else{
				if(map[Y[0]+1][X[0]]=='$'){
					eat(map);
					++bl;
				}   //吃吃吃 
				
				map[Y[j]][X[j]]=' ';
				if(j!=0){
				map[Y[0]][X[0]]='X';
				
				for(int i=j;i>0;--i){
					Y[i]=Y[i-1];
					X[i]=X[i-1];
					}
				}    								//坐标挪位 
				
				map[++Y[0]][X[0]]='H';
				if(bl) rand_map(map);
				print_map(map);
			}
			break;
		}
}
}
int main(){
	char map[12][13]={     //map[列][行] 
	"************",
	"*H         *",
	"*      $   *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"************"};
	print_map(map);
	while(game_over){
		move(map);
		if(game_over==0) print_map(map_1);
	}
	return 0;
}
