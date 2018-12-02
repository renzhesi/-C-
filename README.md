# -C-
软件工程过程
#include <stdio.h>
#include <string.h>
#include<stdlib.h>
#include<conio.h>
#define N 100
///////////////////////////////////////////////
//声明
void shouye();
int yanzheng(char mima1[]);
int zhucaidan();
void shuru();
void baocun();
void duqu();
void paixu();
void chazhao();
void xiugai();
void zengjian();
//////////////////////////////////
//定义结构体
struct shang
{
	char  xingming[10];
	char  xuehao[10];
	char  xingbie[10];
	char  chushengriqi[10];
	char  banji[10];
	char  dianhua[10];
}xuesheng[N];

int ge=0;/////////////////////////////////////
//主函数
void main()
{
	int n;
	char mima1[7]={"111000"};//初始密码
	shouye();//主页面显示
	n=yanzheng(mima1);//验证密码
	switch(n)
	{
	case 0: printf("\n对不起，密码连续错误3次，自动退出系统，谢谢使用\n");
		break;
	case 1: zhucaidan();//显示主菜单并进行选择
		break;
	}
	printf("退出成功，谢谢使用!\n");
	exit(0);
}
////////////////////////////////////
//显示作者信息
void shouye()
{
	printf("\n\n\t\t*******************************************\n");
	printf("\t\t**       欢迎进入学生学籍管理系统        **\n");
	printf("\t\t**           班级:   软件17-2            **\n");
	printf("\t\t**           姓名:     曹力文            **\n");
	printf("\t\t**           学号：1714010201            **\n");
	printf("\t\t**           指导老师：马超              **\n");
	printf("\t\t**           时间:   2017-12-21          **\n");
    printf("\t\t*******************************************\n");
}
//////////////////////////////////////
//密码验证
int yanzheng(char mima1[])
{
	int i=0,k=3,m;
	char mima2[7];
	printf("请输入密码：");
	for(m=0;m<6;m++)
	{
		mima2[m]=getch();//输入密码但不显示密码
		putchar('*');//显示星号
	}
	mima2[6]='\0';//添加串结束标志
	printf("\n");
	for(i=0;k!=0;i++)
	{
		if(strcmp(mima2,mima1)==0)//比较密码是否相同，相同则进行此步
		{
			printf("密码正确,欢迎进入学生管理系统\n");
			system("pause");//屏幕暂停
			return 1;
		}
		else //密码不相同，进行此步
		{
			--k;
			if(k==0)
			{
				return 0;
			}
			printf("\n密码错误,你还有%d次输入的机会\n请再次输入密码：",k);
			for(m=0;m<6;m++)
			{
				mima2[m]=getch();//输入密码，但不显示密码
				putchar('*');//显示星号
			}
			mima2[6]='\0';//添加串结束标志
			printf("\n");
		}
	}
	return 0;
}
///////////////////////////////////////
//显示主菜单
int zhucaidan()
{

	int z;
	while(1)
	{
		system("cls");
		printf("\n\n\t\t*******************************************\n");
		printf("\t\t**           1.学籍增加                  **\n");
		printf("\t\t**           2.学籍查看                  **\n");
		printf("\t\t**           3.学籍查询                  **\n");
		printf("\t\t**           4.学籍学号排序              **\n");
		printf("\t\t**           5.学籍的删除与修改          **\n");
		printf("\t\t**           6.退出系统                  **\n");
		printf("\t\t*******************************************\n");

		printf("\t\t请输入选项：");
		scanf("%d",&z);
		switch(z)
		{
		case 1: shuru();
			break;
		case 2:duqu();
			break;
		case 3:chazhao();
			break;
		case 4:paixu();//排序
			break;
		case 5: xiugai();
			break;
		case 6: system("cls");//清屏
			printf("退出系统 \n");
			return 0;
		default:printf("无此选项\n");
			system("pause");
			break;
		}
	}
}
void shuru()
{
	int i=0,n=0;
	system("cls");//清屏
	printf("学籍信息录入  \n");
	for(i=0;i<N;i++)
	{
		printf("输入学生姓名：");
		scanf(" %s", xuesheng[i].xingming);
		printf("输入学生学号：");
		scanf(" %s", xuesheng[i].xuehao);
		printf("输入学生性别：");
		scanf(" %s", xuesheng[i].xingbie);
		printf("输入所在班级：");
		scanf(" %s", xuesheng[i].banji);
		printf("输入出生日期：");
		scanf(" %s", xuesheng[i].chushengriqi);
		printf("输入电话：");
		scanf(" %s", xuesheng[i].dianhua);
		baocun();
		ge++;
		system("cls");//清屏
		printf("\n\n\t\t***************************************\n");
		printf("\t\t**                                   **\n");
		printf("\t\t**  1.继续录入       0.保存并跳出    **\n");
		printf("\t\t**                                   **\n");
		printf("\t\t***************************************\n");
		printf("\t\t请输入选项：\b");
		scanf("%d",&n);
		if(n==1)//继续录入数据
			continue;
		if(n==0)//跳出本循环
		{
			system("cls");
			break;//清屏
		}
	}
}
//////////////////////////////////////////
//保存数据函数
void baocun()
{
	FILE *fp;
	int i;
	if((fp=fopen("xuesheng.dat","wb"))==NULL)
	{
		printf("不能打开文件\n");
		return;
	}
	for(i=0;i<N;i++)
		if(fwrite (&xuesheng[i],sizeof(struct shang),1,fp)!=1)
			printf("文件写入错误\n");
		fclose(fp);
}
void duqu()
{
	FILE *fp;
	int i;
	system("cls");//清屏
	printf("学生信息浏览  \n");
	if((fp=fopen("xuesheng.dat","rb"))==NULL)//打开文件
	{
		printf("不能打开文件\n");
	}
	printf("学生姓名        学生学号         性别         班级             出生日期         电话\n");
	for(i=0;i<ge;i++)
	{
		fread(&xuesheng[i],sizeof(struct shang),1,fp);
		printf("%-16s%-17s%-15s%-16s%-15s%-17s\n",xuesheng[i].xingming,xuesheng[i].xuehao,xuesheng[i].xingbie,xuesheng[i].banji,xuesheng[i].chushengriqi,xuesheng[i].dianhua);
	}
	fclose(fp);
	system("pause");
}
void paixu()
{
	struct shang temp;
	int i,j,n;
	system("cls");//清屏
	printf("根据学生学号排序  \n");
	printf("学生姓名        学生学号         性别        班级          出生日期            电话\n");
	for (i=0;i<ge;i++)
		for(j=i+1;j<ge;j++)
			if(xuesheng[i].xuehao<xuesheng[j].xuehao)
			{
				temp=xuesheng[i];
				xuesheng[i]=xuesheng[j];
				xuesheng[j]=temp;
			}
			for(i=0;i<ge;i++)
			{
				printf("%-16s%-17s%-15s%-16s%-15s%-17s\n",xuesheng[i].xingming,xuesheng[i].xuehao,xuesheng[i].xingbie,xuesheng[i].banji,xuesheng[i].chushengriqi,xuesheng[i].dianhua);
			}
			printf("选择0退出排序系统 _\b");
			scanf("%d",&n);
			if(n==0)//跳出本循环
			{
				system("cls");//清屏
				zhucaidan();//返回主菜单
			}
}
void chazhao()
{
	int i,n,m,a=0;
	char xingming_1[10],xuehao_1[10];
	FILE *fp;
	system("cls");//清屏
	printf("学生学籍查询  \n");
	if((fp=fopen("xuesheng.dat","r"))==NULL)//打开文件
	{
		printf("不能打开文件\n");
	}
	printf("\n\n\t\t***************************************\n");
	printf("\t\t**             查找学生              **\n");
	printf("\t\t**           1.姓名查找              **\n");
	printf("\t\t**           2.学号查找              **\n");
	printf("\t\t**           0.退出查询              **\n");
	printf("\t\t***************************************\n");
	printf("\t\t请输入选项：");
	scanf("%d",&n);
	system("cls");//清屏
	switch(n)
	{
	case 1: printf("请输入你所要查找的学生姓名\n");
		scanf("%s",xingming_1);
		for(i=0;i<ge;i++)
		{
			if(strcmp(xingming_1,xuesheng[i].xingming) == 0)
			{
				a=1;
				printf("学生姓名        学生学号        性别         班级           出生日期        电话\n");
				printf("%-16s%-17s%-15s%-16s%-15s%-17s\n",xuesheng[i].xingming,xuesheng[i].xuehao,xuesheng[i].xingbie,xuesheng[i].banji,xuesheng[i].chushengriqi,xuesheng[i].dianhua);
			}
		}
		if(a==0)
		{
			printf("**         查无此学生        \n**");
			printf("输入任意键返回:\n");
			getch();
		}
		break;
	case 2: printf("请输入你所要查找的学生学号\n");
		scanf("%s",xuehao_1);
		for(i=0;i<ge;i++)
		{
			if(strcmp(xuehao_1,xuesheng[i].xuehao) == 0)
			{
				a=1;
				printf("学生姓名        学生学号         性别         班级           出生日期         电话\n");
				printf("%-16s%-17s%-15s%-16s%-15s%-17s\n",xuesheng[i].xingming,xuesheng[i].xuehao,xuesheng[i].xingbie,xuesheng[i].banji,xuesheng[i].chushengriqi,xuesheng[i].dianhua);
			}

		}
		if(a==0)
		{
			printf("**         查无此学生        **\n");
			printf("输入任意键返回:\n");
			getch();
		}
		break;
	case 0:	system("cls");//清屏
		zhucaidan();//返回主菜单
	}
	printf("\n\n\t\t***************************************\n");
	printf("\t\t**                                   **\n");
	printf("\t\t**     1.继续查询       0.退出       **\n");
	printf("\t\t**                                   **\n");
	printf("\t\t***************************************\n");
	printf("\t\t请输入选项：");
	scanf("%d",&m);
	if(m==1)//继续查询数据
		chazhao();
	if(m==0)//跳出本循环
	{
		system("cls");//清屏
		zhucaidan();//返回主菜单
	}
}
void xiugai()
{
	int  i,k=0;//变量
	int  n,m;//选择键
	char str[10];
	system("cls");//清屏
	printf("学生学籍的删除与修改  \n");
	printf("\n\n\t\t***************************************\n");
	printf("\t\t**                                   **\n");
	printf("\t\t**          删除和更改学籍           **\n");
	printf("\t\t**                                   **\n");
	printf("\t\t***************************************\n");
	printf("\t\t请输入你要删除和更改的学生姓名或是学号");
	scanf("%s",str);
	system("cls");//请屏
	for(i=0;i<ge;i++)
	{
		if((strcmp(str,xuesheng[i].xingming) == 0) || (strcmp(str,xuesheng[i].xuehao) == 0))
		{
			k=i;
			printf("学生姓名        学生学号        性别         班级           出生日期            电话\n");
			printf("%-16s%-17s%-15s%-16s%-15s%-17s\n",xuesheng[i].xingming,xuesheng[i].xuehao,xuesheng[i].xingbie,xuesheng[i].banji,xuesheng[i].chushengriqi,xuesheng[i].dianhua);

		}
	}
	printf("\n\n\t\t***************************************\n");
	printf("\t\t**                                   **\n");
	printf("\t\t**            1.删除学籍             **\n");
	printf("\t\t**                                   **\n");
	printf("\t\t**            2.更改学籍             **\n");
	printf("\t\t**                                   **\n");
	printf("\t\t***************************************\n");
	printf("\t\t请输入选项：\b");
	scanf("%d",&n);
	switch(n)
	{
	case 1:
		for(i=k;i<ge-1;i++)
		{
			xuesheng[i]=xuesheng[i+1];

		}
		system("cls");//清屏
		printf("你选择的学籍已删除信息成功！\n");
		ge--;
		break;
	case 2:printf("对学籍进行修改！\n");
		i = k;
		printf("输入新的学生姓名：");
		scanf(" %s", xuesheng[i].xingming);
		printf("输入新的学生学号：");
		scanf(" %s", xuesheng[i].xuehao);
		printf("输入新的性别：");
		scanf(" %s", xuesheng[i].xingbie);
		printf("输入新的班级：");
		scanf(" %s", xuesheng[i].banji);
		printf("输入新的出生日期：");
		scanf(" %s", xuesheng[i].chushengriqi);
		printf("输入新的电话：");
		scanf(" %s", xuesheng[i].dianhua);
		system("cls");//清屏
		printf("你选择的学籍已更改信息成功！\n");
		printf("学生姓名        学生学号          性别         班级              出生日期            电话\n");
		printf("%-16s%-17s%-15s%-16s%-15s%-17s\n",xuesheng[i].xingming,xuesheng[i].xuehao,xuesheng[i].xingbie,xuesheng[i].banji,xuesheng[i].chushengriqi,xuesheng[i].dianhua);
		break;
	}
	baocun();
	printf("\n\n\t\t***************************************\n");
	printf("\t\t**                                   **\n");
	printf("\t\t**   1.继续删除或修改       0.退出   **\n");
	printf("\t\t**                                   **\n");
	printf("\t\t***************************************\n");
	printf("\t\t请输入选项：");
	scanf("%d",&m);
	if(m==1)
	{
		system("cls");//清屏
		xiugai();
	}
	if(m==2)//跳出本循环
	{
		system("cls");//清屏
		zhucaidan();//返回主菜单
	}
}
