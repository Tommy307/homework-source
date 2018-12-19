#智能蛇实验报告  
*与贪吃蛇实验的不同之处*  
需要设计一个时间轴，人工蛇每移动依次，时间轴上的时间加1  
智能蛇则依据事先设计好的趋向“食物”的算法，时间轴上的时间每加1，它就会自动相应地走一步。  
  
    

     
       
##程序如下：（由于加入了智能蛇，所以在原先的基础上增大了游戏范围）
#include <stdio.h>
#include <string.h>
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
#include <termios.h>
#include <unistd.h>

static struct termios ori_attr, cur_attr;

static __inline 
int tty_reset(void)
{
        if (tcsetattr(STDIN_FILENO, TCSANOW, &ori_attr) != 0)
                return -1;

        return 0;
}


static __inline
int tty_set(void)
{
        
        if ( tcgetattr(STDIN_FILENO, &ori_attr) )
                return -1;
        
        memcpy(&cur_attr, &ori_attr, sizeof(cur_attr) );
        cur_attr.c_lflag &= ~ICANON;
//        cur_attr.c_lflag |= ECHO;
        cur_attr.c_lflag &= ~ECHO;
        cur_attr.c_cc[VMIN] = 1;
        cur_attr.c_cc[VTIME] = 0;

        if (tcsetattr(STDIN_FILENO, TCSANOW, &cur_attr) != 0)
                return -1;

        return 0;
}

static __inline
int kbhit(void) 
{
                   
        fd_set rfds;
        struct timeval tv;
        int retval;

        /* Watch stdin (fd 0) to see when it has input. */
        FD_ZERO(&rfds);
        FD_SET(0, &rfds);
        /* Wait up to five seconds. */
        tv.tv_sec  = 0;
        tv.tv_usec = 0;

        retval = select(1, &rfds, NULL, NULL, &tv);
        /* Don't rely on the value of tv now! */

        if (retval == -1) {
                perror("select()");
                return 0;
        } else if (retval)
                return 1;
        /* FD_ISSET(0, &rfds) will be true. */
        else
                return 0;
        return 0;
}

int X[200]={1},Y[100]={1},game_over=1,j=0;
int s[]={24,15,7,22,14,1,6,12,19,8,21,5,17,3,10,9,4,2,3,5,9,5,21,6,23,2,5,4,12,3,10,1,3,2,21,5,10,6,27,9,8,1,15,10,18,10,9,4,12,3,5,9,5,11,6,3,2,5,4,22,3,10,
1,3,7,13,4,10,6,7,9,8,4,5,7,3,10,9,4,22,3,5,9,5,1,6,3,2,15,4,2,3,10,1,3,7,17,4,10,6,27,9,8,21,5,7,3,10,9,4,2,13,5,9,25,1,6,3,5,5,4,2,3,10};
int w[]={24,15,67,22,14,1,96,12,19,28,21,5,17,3,10,9,44,52,63,75,89,55,21,6,23,2,5,4,12,23,10,11,43,92,21,5,10,6,27,9,8,1,15,10,18,10,9,4,12,3,5,79,5,11,6,3,2,5,4,22,3,10,
41,3,7,13,4,10,6,57,9,8,4,5,7,3,10,9,4,22,43,5,9,5,61,6,3,2,15,4,2,3,10,1,3,7,17,4,10,6,27,9,8,21,5,7,3,14,9,4,2,13,5,9,25,1,6,3,5,5,4,2,63,10};
char map_1[][101]={
	"**************************************************************************************************",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                       @@@@@@    @@@@@@   @@@@ @@@@    @@@@@@                                   *",
	"*                       @        @     @   @   @   @    @    @                                   *",
	"*                       @   @@@  @     @   @   @   @    @@@@@@                                   *",
	"*                       @    @   @     @   @   @   @    @                                        *",
	"*                       @@@@@@    @@@@@@@  @   @   @    @@@@@@                                   *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                             @@@@@    @     @   @@@@@@  @   @                   *",
	"*                                            @     @   @     @   @    @   @ @                    *",
	"*                                            @     @   @     @   @@@@@@   @@                     *",
	"*                                            @     @    @   @    @        @                      *",
	"*                                             @@@@@       @      @@@@@@   @                      *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"**************************************************************************************************"};
int rand_map(char map[][101]){
	int t=0;
	int yer=1;
	while(yer){
	if(map[s[j+t]][w[j+t+1]]!='H'&&map[s[j+t]][w[j+t+1]]!='X'){
			map[s[j+t]][w[j+t+1]]='$';--yer;}
	else ++t;
	}
}
void print_map(char s[][101]){
	for(int i=0;i<28;++i)
	printf("%s\n",s[i]);
}

void eat(char map[][101]){
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
void move(char map[][101]){
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
			if(X[0]+1==99||map[Y[0]][X[0]+1]=='X'){
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
			if(Y[0]+1==27||map[Y[0]+1][X[0]]=='X'){
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
}//将你的 snake 代码放在这里

int main()
{
        //设置终端进入非缓冲状态
        int tty_set_flag;
        tty_set_flag = tty_set();

        	char map[28][101]={     //map[纵坐标][横坐标] 
	"**************************************************************************************************",
	"*H                                                                                               *",
	"*      $                                                                                         *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"*                                                                                                *",
	"**************************************************************************************************"};
	print_map(map);
	while(game_over){
		move(map);
		if(game_over==0) print_map(map_1);
	}//将你的 snake 代码放在这里
        printf("pressed `q` to quit!\n");
        while(1) {

                if( kbhit() ) {
                        const int key = getchar();
                        printf("%c pressed\n", key);
                        if(key == 'q')
                                break;
                } else {
                       ;// fprintf(stderr, "<no key detected>\n");
                }
        }

        //恢复终端设置
        if(tty_set_flag == 0) 
                tty_reset();
        return 0;
}
