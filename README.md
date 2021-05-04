#include<stdio.h> 
struct student 
{ 
 char name[50]; 
 int id; 
 char mobile[50]; 
 char trimesterName[50]; 
 char cgpa[50]; 
}; 
int main() 
{ 
 printf("<--:Student Record Management System:-->"); 
 printf("\nPress any key to continue."); 
 getch(); 
 menu(); 
 return 0; } 
void menu() 
{ 
 int choice; 
 system("cls"); 
 printf("<--:MENU:-->"); 
 printf("\nEnter appropriate number to perform following task."); 
 printf("\n1 : Add Record."); 
 printf("\n2 : View Record."); 
 printf("\n3 : Search Record."); 
 printf("\n4 : Delete."); 
 printf("\n5 : Exit."); 
 printf("\nEnter your choice :"); 
 scanf("%d",&choice); 
 switch(choice) 
 { 
 case 1: 
 add(); 
 break; 
 
 case 2: 
 view(); 
 break; 
 
 case 3: 
 search(); 
 break; 
 
 case 4: 
 deleterec(); 
 break; 
 
 case 5: 
 exit(1); 
 break; 
 
 default:  printf("\nInvalid Choice."); 
 } 
} 
 
void add() 
{ 
 FILE *fp; 
 struct student std; 
 char another ='y'; 
 system("cls"); 
 
 fp = fopen("record.txt","ab+"); 
 if(fp == NULL){ 
 printf("Error opening file"); 
 exit(1); 
 } 
 fflush(stdin); 
 while(another == 'y') 
 { 
 printf("Enter details of student."); 
 printf("\nEnter Name : "); 
 gets(std.name); 
 printf("\nEnter ID No : "); 
 scanf("%d",&std.id); 
 fflush(stdin); 
 printf("\nEnter Mobile Number : "); 
 gets(std.mobile); 
 printf("\nEnter Trimester Name : "); 
 gets(std.trimesterName); 
 printf("\nEnter Branch : "); 
 gets(std.cgpa); 
 fwrite(&std,sizeof(std),1,fp); 
 printf("\nWant to add of another record? Then press 'y' else 'n'."); 
 another = getch(); 
 system("cls"); 
 fflush(stdin); 
 }  fclose(fp); 
 menu(); 
} 
 
 
void view() 
{ 
 FILE *fp; 
 int i=1; 
 struct student std; 
 system("cls"); 
 printf("S.No Name ID Mobile no. Trimester CGPA\n"); 
 printf("------------------------------------------------------------------------\n"); 
 fp = fopen("record.txt","rb+"); 
 if(fp == NULL){ 
 printf("\nError opening file."); 
 exit(1); 
 } 
 while(fread(&std,sizeof(std),1,fp) == 1){ 
 printf("\n%-7d%-15s%-13d%-15s%-15s%-
15s",i,std.name,std.id,std.mobile,std.trimesterName,std.cgpa); 
 i++; 
 } 
 fclose(fp); 
 printf("\nPress any key to continue."); 
 getch(); 
 menu(); 
} 
void search() 
{ 
 FILE *fp; 
 struct student std; 
 char stname[20]; 
 system("cls"); 
 printf("\n<--:SEARCH RECORD:-->"); 
 printf("\nEnter name of student : "); 
 fflush(stdin);  gets(stname); 
 fp = fopen("record.txt","rb+"); 
 if(fp == NULL){ 
 printf("Error opening file"); 
 exit(1); 
 } 
 while(fread(&std,sizeof(std),1,fp ) == 1){ 
 if(strcmp(stname,std.name) == 0){ 
 printf("\nName : %s",std.name); 
 printf("\nID No : %d",std.id); 
 printf("\nMobile Number : %s",std.mobile); 
 printf("\nTrimester Name : %s",std.trimesterName); 
 printf("\nCGPA : %s",std.cgpa); 
 } 
 } 
 fclose(fp); 
 printf("\nPress any key to continue."); 
 getch(); 
 menu(); 
} 
void deleterec() 
{ 
 char stname[20]; 
 FILE *fp,*ft; 
 struct student std; 
 system("cls"); 
 printf("\n<--:DELETE RECORD:-->"); 
 printf("\nEnter name of student to delete record : "); 
 fflush(stdin); 
 gets(stname); 
 fp = fopen("record.txt","rb+"); 
 if(fp == NULL){ 
 printf("\nError opening file"); 
 exit(1); 
 } 
 ft = fopen("temp.txt","wb+"); 
 if(ft == NULL){  printf("\nError opening file"); 
 exit(1); 
 } 
 while(fread(&std,sizeof(std),1,fp) == 1){ 
 if(strcmp(stname,std.name)!=0) 
 fwrite(&std,sizeof(std),1,ft); 
 } 
 fclose(fp); 
 fclose(ft); 
 remove("record.txt"); 
 rename("temp.txt","record.txt"); 
 printf("\nPress any key to continue."); 
 getch(); 
 menu(); 
} 
