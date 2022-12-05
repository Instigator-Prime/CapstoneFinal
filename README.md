#include<stdio.h>

typedef struct hall{
       int rnum;
      char name[35];
      char location[30];
      int roomnum;

}hall;

int low=1, up=350;

void create(){

   hall h;
   FILE *fp = fopen("hall.txt","a+");

   printf("Enter Last part of ID : ");
   scanf("%d",&h.rnum);
   printf("Enter your name here : ");
   scanf("%s",h.name);
   printf("Enter Location : ");
   scanf("%s",h.location);
   h.roomnum = getRoomNo(((rand()%(up-low+1))+low));
   if (h.roomnum!=0)
   fwrite(&h,sizeof(hall),1,fp);

   fclose(fp);

}

int getRoomNo(int roomnum){
    int allocated = 0;
    FILE *fp = fopen("hall.txt","r");
    hall h1;
    while(fread(&h1,sizeof(hall),1,fp))
    {


    if(h1.roomnum == roomnum){
            allocated=1;


       }
    }
if (allocated == 0)
        return roomnum;
else
    return getRoomNo(((rand()%(up-low+1))+low));

fclose(fp);
}


void display(){
    hall h1;
    FILE *fp = fopen("hall.txt","r");
    printf("%-10s%-20s%-15s%-10s\n","ID-Index","Name","location","Room No");
    while(fread(&h1,sizeof(hall),1,fp))
    printf("%-10d%-20s%-15s%-10d\n",h1.rnum,h1.name,h1.location,h1.roomnum);



}


int main(){
   int character;
   do{
    printf("\n1.Room Allocation");
    printf("\n2.Details");
    printf("\n0.EXIT");
    printf("\nEnter the choice : ");
    scanf("%d",&character);

    switch(character){
    case 1:
        create();
        break;
    case 2:
        display();
        break;
    case 0: printf("Thanks for using this code");
    }
   }while(character!=0);
}
