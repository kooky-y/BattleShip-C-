# BattleShip-C- //Code
//BattleShip Game in C++
#include <iostream>
#include <fstream>
#include <time.h>
#include <cstdlib>
#include <string>
#include <windows.h>
#include <mmsystem.h>
using namespace std;
const int size = 5;
int ShipSize[size]={5,4,3,3,2};
string array[11][11];
string array_15[16][16];
string array_20[21][21];
string Placement10[11][11];
string Placement15[16][16];
string Placement20[21][21];
string user10[11][11];
string user15[16][16];
string user20[21][21];
int UserCheckY; //To check the co-ordinates of Missile.
int ComputerCheckX; //To check the co-ordinates of Missile.
int UserCheckX;//To check the co-ordinates of Missile.
int ComputerCheckY;//To check the co-ordinates of Missile.
//For Printing the Board
void ShowOpponentBoard(int &menu){
//10x10 Board (Easy Peasy Level)
string number[20]={"0","1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19"};
int num = 0;
int num1 = 0;
int num20 = 0;


ofstream gameboard;
ofstream gameboard15x15;
ofstream gameboard20x20;


switch (menu){

    case 1:
     gameboard.open("original10.txt");
int row, col;



for (row = 0; row < 11; row++) {
for (col = 0; col < 11; col++) {
if (row == 0 && col == 0){
array[row][col] = "@";
Placement10[row][col]= "@";
user10[row][col]="@";
}
else if (row == 0 && col > 0) {
array[row][col] = number[num];
Placement10[row][col]=number[num];
user10[row][col]=number[num];
++num;
}
else if (col == 0 && row >= 1) {
array[row][col] = row + 64;
Placement10[row][col]= row+64;
user10[row][col]=row+64;
}
else{
array[row][col] = "o";
Placement10[row][col]="o";
user10[row][col]="o";
}
}
}
for (int x = 0; x < 11; x++) {
for (int y = 0; y < 11; y++) {
  gameboard << array[x][y] << " ";
}
gameboard << endl;
}
break;

//15x15 (A bit hard Bruh)
//
//
//
  //Array of 15x15
  case 2:


gameboard15x15.open("original15.txt");

for (row = 0; row < 16; row++) {
for (col = 0; col < 16; col++) {
if (row == 0 && col == 0){
array_15[row][col] = "@";
Placement15[row][col]="@";
user15[row][col]="@";
}
else if (row == 0 && col > 0) {
array_15[row][col] = number[num1];
Placement15[row][col]=number[num1];
user15[row][col]=number[num1];
++num1;
}
else if (col == 0 && row >= 1) {
array_15[row][col] = row + 64;
Placement15[row][col]=row + 64;
user15[row][col]=row + 64;
}
else{
array_15[row][col] = "o";
Placement15[row][col]="o";
user15[row][col]="o";
}
}
}
for (int x = 0; x < 16; x++) {
for (int y = 0; y < 16; y++) {
           if (y>=10 && x!=0){
                gameboard15x15 << array_15[x][y] << "  ";
}
else
            gameboard15x15 << array_15[x][y] << " ";

}
gameboard15x15 << endl;

}
break;

//20x20 (Here comes the Extreme Level HurB"
        //
        //
        //
case 3:


gameboard20x20.open("original20.txt");

for (row = 0; row < 21; row++) {
for (col = 0; col < 21; col++) {
if (row == 0 && col == 0){
array_20[row][col] = "@";
Placement20[row][col]="@";
user10[row][col]="@";
}
else if (row == 0 && col > 0) {
array_20[row][col] = number[num20];
Placement20[row][col]=number[num20];
user20[row][col]=number[num20];
++num20;
}
else if (col == 0 && row >= 1) {
array_20[row][col] = row + 64;
Placement20[row][col]=row+64;
user20[row][col]=row+64;
}
else{
array_20[row][col] = "o";
Placement20[row][col]="o";
user20[row][col]="o";
}
}
}
for (int x = 0; x < 21; x++) {
for (int y = 0; y < 21; y++) {
           if (y>=10 && x!=0){
                gameboard20x20 << array_20[x][y] << "  ";
}
else
            gameboard20x20 << array_20[x][y] << " ";

}
gameboard20x20 << endl;

}
break;

}
}
//End oF ShowOpponentBoard
void ShipsPlacement10(){ //Placement of 10x10 Computer Ships.
    int row,col;
    int direction;
for (int i = 0;i<size;i++){
        Sleep(500);
srand(time(0));
direction = rand()%2; //1 for Vertical Positioning and 0 for Horizontal Positioning.
AirCarrier:
row = (rand()%10)+1;
col = (rand()%10)+1;
int counter=0;
if(ShipSize[i]==5){ //Placement of Air Carrier.
    if(direction == 1 && row<=5){
    for(int j = row;j<row+5;j++){
        for(int k = col;k<=col;k++){
            Placement10[j][k]="A";
        }
    }
    }
    else if (direction==0 && col<=5){
        for (int j = row;j<=row;j++){
            for(int k = col;k<col+5;k++){
                Placement10[j][k]="A";
            }
        }
    }
    else
        goto AirCarrier;
} //End of Air Carrier
else if(ShipSize[i]==4){   //PlaceMent of BattleShip.
    if(direction == 1 && row <=6){
        for(int a=0;a<4;a++){
            if(Placement10[a+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                Placement10[g+row][col]="B";
            }
        }

    }
    else if(direction==0 && col<=6){

     for(int a=0;a<4;a++){
            if(Placement10[row][a+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                Placement10[row][g+col]="B";
            }
        }

    }
    else{
        goto AirCarrier;
    }


}//end Of BattleShip.
else if(i==2){   //PlaceMent of Cruiser Ship.
    if(direction == 1 && row <=7){
        for(int r=0;r<3;r++){
            if(Placement10[r+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                Placement10[t+row][col]="C";
            }
        }

    }
    else if(direction==0 && col<=7){

     for(int r=0;r<3;r++){
            if(Placement10[row][r+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                Placement10[row][t+col]="C";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}
//end Of Cruiser Ship.
else if(i==3){   //Submarin+e Placement
    if(direction == 1 && row <=7){
        for(int w=0;w<3;w++){
            if(Placement10[w+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                Placement10[q+row][col]="S";
            }
        }

    }
    else if(direction==0 && col<=7){

     for(int w=0;w<3;w++){
            if(Placement10[row][w+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                Placement10[row][q+col]="S";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Submarine
else if(ShipSize[i]==2){   //PlaceMent of Destroyer
    if(direction == 1 && row <=8){
        for(int m=0;m<2;m++){
            if(Placement10[m+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                Placement10[n+row][col]="D";
            }
        }

    }
    else if(direction==0 && col<=8){

     for(int m=0;m<2;m++){
            if(Placement10[row][m+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                Placement10[row][n+col]="D";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Destroyer Ship.

}

ofstream placementof10("random10.txt");
for (int x = 0; x < 11; x++) {
for (int y = 0; y < 11; y++) {
  placementof10 << Placement10[x][y] << " ";
}
placementof10 << endl;
}
cout << "10x10 Grid Computer Ships Has been Placed Successfully!" << endl << endl;
}
void ShipsPlacement15(){//Placement of 15x15 Computer ships
    int row,col;
    int direction;
for (int i = 0;i<size;i++){
        Sleep(500);
srand(time(0));
direction = rand()%2; //1 for Vertical Positioning and 0 for Horizontal Positioning.
AirCarrier:
row = (rand()%15)+1;
col = (rand()%15)+1;
int counter=0;
if(ShipSize[i]==5){ //Placement of Air Carrier.
    if(direction == 1 && row<=10){
    for(int j = row;j<row+5;j++){
        for(int k = col;k<=col;k++){
            Placement15[j][k]="A";
        }
    }
    }
    else if (direction==0 && col<=10){
        for (int j = row;j<=row;j++){
            for(int k = col;k<col+5;k++){
                Placement15[j][k]="A";
            }
        }
    }
    else
        goto AirCarrier;
} //End of Air Carrier
else if(ShipSize[i]==4){   //PlaceMent of BattleShip.
    if(direction == 1 && row <=11){
        for(int a=0;a<4;a++){
            if(Placement15[a+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                Placement15[g+row][col]="B";
            }
        }

    }
    else if(direction==0 && col<=11){

     for(int a=0;a<4;a++){
            if(Placement15[row][a+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                Placement15[row][g+col]="B";
            }
        }

    }
    else{
        goto AirCarrier;
    }


}//end Of BattleShip.
else if(i==2){   //PlaceMent of Cruiser Ship.
    if(direction == 1 && row <=12){
        for(int r=0;r<3;r++){
            if(Placement15[r+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                Placement15[t+row][col]="C";
            }
        }

    }
    else if(direction==0 && col<=12){

     for(int r=0;r<3;r++){
            if(Placement15[row][r+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                Placement15[row][t+col]="C";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}
//end Of Cruiser Ship.
else if(i==3){   //Submarice Placement
    if(direction == 1 && row <=12){
        for(int w=0;w<3;w++){
            if(Placement15[w+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                Placement15[q+row][col]="S";
            }
        }

    }
    else if(direction==0 && col<=12){

     for(int w=0;w<3;w++){
            if(Placement15[row][w+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                Placement15[row][q+col]="S";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Submarine
else if(ShipSize[i]==2){   //PlaceMent of Destroyer
    if(direction == 1 && row <=13){
        for(int m=0;m<2;m++){
            if(Placement15[m+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                Placement15[n+row][col]="D";
            }
        }

    }
    else if(direction==0 && col<=13){

     for(int m=0;m<2;m++){
            if(Placement15[row][m+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                Placement15[row][n+col]="D";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Destroyer Ship.

}

ofstream placementof15("random15.txt");
for (int x = 0; x < 16; x++) {
for (int y = 0; y < 16; y++) {
           if (y>=10 && x!=0){
                placementof15 << Placement15[x][y] << "  ";
}
else
            placementof15 << Placement15[x][y] << " ";

}
placementof15 << endl;

}
cout << "15x15 Grid Computer Ships Has been Placed Successfully!" << endl << endl;
}
void ShipsPlacement20(){//Placement of 20x20 Computer ships
    int row,col;
    int direction;
for (int i = 0;i<size;i++){
    Sleep(500);
srand(time(0));
direction = rand()%2; //1 for Vertical Positioning and 0 for Horizontal Positioning.
AirCarrier:
row = (rand()%20)+1;
col = (rand()%20)+1;
int counter=0;
if(ShipSize[i]==5){ //Placement of Air Carrier.
    if(direction == 1 && row<=15){
    for(int j = row;j<row+5;j++){
        for(int k = col;k<=col;k++){
            Placement20[j][k]="A";
        }
    }
    }
    else if (direction==0 && col<=15){
        for (int j = row;j<=row;j++){
            for(int k = col;k<col+5;k++){
                Placement20[j][k]="A";
            }
        }
    }
    else
        goto AirCarrier;
} //End of Air Carrier
else if(ShipSize[i]==4){   //PlaceMent of BattleShip.
    if(direction == 1 && row <=16){
        for(int a=0;a<4;a++){
            if(Placement20[a+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                Placement20[g+row][col]="B";
            }
        }

    }
    else if(direction==0 && col<=16){

     for(int a=0;a<4;a++){
            if(Placement20[row][a+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                Placement20[row][g+col]="B";
            }
        }

    }
    else{
        goto AirCarrier;
    }


}//end Of BattleShip.
else if(i==2){   //PlaceMent of Cruiser Ship.
    if(direction == 1 && row <=17){
        for(int r=0;r<3;r++){
            if(Placement20[r+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                Placement20[t+row][col]="C";
            }
        }

    }
    else if(direction==0 && col<=17){

     for(int r=0;r<3;r++){
            if(Placement20[row][r+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                Placement20[row][t+col]="C";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}
//end Of Cruiser Ship.
else if(i==3){   //Submarice Placement
    if(direction == 1 && row <=17){
        for(int w=0;w<3;w++){
            if(Placement20[w+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                Placement20[q+row][col]="S";
            }
        }

    }
    else if(direction==0 && col<=17){

     for(int w=0;w<3;w++){
            if(Placement20[row][w+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                Placement20[row][q+col]="S";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Submarine
else if(ShipSize[i]==2){   //PlaceMent of Destroyer
    if(direction == 1 && row <=18){
        for(int m=0;m<2;m++){
            if(Placement20[m+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                Placement20[n+row][col]="D";
            }
        }

    }
    else if(direction==0 && col<=18){

     for(int m=0;m<2;m++){
            if(Placement20[row][m+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                Placement20[row][n+col]="D";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Destroyer Ship.

}

ofstream placementof20("random20.txt");
for (int x = 0; x < 21; x++) {
for (int y = 0; y < 21; y++) {
           if (y>=10 && x!=0){
                placementof20 << Placement20[x][y] << "  ";
}
else
            placementof20 << Placement20[x][y] << " ";

}
placementof20 << endl;

}
cout << "20x20 Grid Computer Ships Has been Placed Successfully!" << endl << endl;
}
void UserShip10(){

    int row,col;
    int direction;
for (int i = 0;i<size;i++){
    Sleep(500);
srand(time(0));
direction = rand()%2; //1 for Vertical Positioning and 0 for Horizontal Positioning.
AirCarrier:
row = (rand()%10)+1;
col = (rand()%10)+1;
int counter=0;
if(ShipSize[i]==5){ //Placement of Air Carrier.
    if(direction == 1 && row<=5){
    for(int j = row;j<row+5;j++){
        for(int k = col;k<=col;k++){
            user10[j][k]="A";
        }
    }
    }
    else if (direction==0 && col<=5){
        for (int j = row;j<=row;j++){
            for(int k = col;k<col+5;k++){
                user10[j][k]="A";
            }
        }
    }
    else
        goto AirCarrier;
} //End of Air Carrier
else if(ShipSize[i]==4){   //PlaceMent of BattleShip.
    if(direction == 1 && row <=6){
        for(int a=0;a<4;a++){
            if(user10[a+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                user10[g+row][col]="B";
            }
        }

    }
    else if(direction==0 && col<=6){

     for(int a=0;a<4;a++){
            if(user10[row][a+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                user10[row][g+col]="B";
            }
        }

    }
    else{
        goto AirCarrier;
    }


}//end Of BattleShip.
else if(i==2){   //PlaceMent of Cruiser Ship.
    if(direction == 1 && row <=7){
        for(int r=0;r<3;r++){
            if(user10[r+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                user10[t+row][col]="C";
            }
        }

    }
    else if(direction==0 && col<=7){

     for(int r=0;r<3;r++){
            if(user10[row][r+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                user10[row][t+col]="C";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}
//end Of Cruiser Ship.
else if(i==3){   //Submarice Placement
    if(direction == 1 && row <=7){
        for(int w=0;w<3;w++){
            if(user10[w+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                user10[q+row][col]="S";
            }
        }

    }
    else if(direction==0 && col<=7){

     for(int w=0;w<3;w++){
            if(user10[row][w+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                user10[row][q+col]="S";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Submarine
else if(ShipSize[i]==2){   //PlaceMent of Destroyer
    if(direction == 1 && row <=8){
        for(int m=0;m<2;m++){
            if(user10[m+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                user10[n+row][col]="D";
            }
        }

    }
    else if(direction==0 && col<=8){

     for(int m=0;m<2;m++){
            if(user10[row][m+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                user10[row][n+col]="D";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Destroyer Ship.

}
cout << "Ships of your 10x10 Grid Has been Placed Successfully!" << endl << endl;
for (int x = 0; x < 11; x++) {
for (int y = 0; y < 11; y++) {
  cout  << user10[x][y] << " ";
}
cout << endl;
}
ofstream userof10("user10.txt");
for (int x = 0; x < 11; x++) {
for (int y = 0; y < 11; y++) {
  userof10 << user10[x][y] << " ";
}
userof10 << endl;
}

}
void UserShip15(){
    int row,col;
    int direction;
for (int i = 0;i<size;i++){
Sleep(500);
srand(time(0));
direction = rand()%2; //1 for Vertical Positioning and 0 for Horizontal Positioning.
AirCarrier:
row = (rand()%15)+1;
col = (rand()%15)+1;
int counter=0;
if(ShipSize[i]==5){ //Placement of Air Carrier.
    if(direction == 1 && row<=10){
    for(int j = row;j<row+5;j++){
        for(int k = col;k<=col;k++){
            user15[j][k]="A";
        }
    }
    }
    else if (direction==0 && col<=10){
        for (int j = row;j<=row;j++){
            for(int k = col;k<col+5;k++){
                user15[j][k]="A";
            }
        }
    }
    else
        goto AirCarrier;
} //End of Air Carrier
else if(ShipSize[i]==4){   //PlaceMent of BattleShip.
    if(direction == 1 && row <=11){
        for(int a=0;a<4;a++){
            if(user15[a+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                user15[g+row][col]="B";
            }
        }

    }
    else if(direction==0 && col<=11){

     for(int a=0;a<4;a++){
            if(user15[row][a+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                user15[row][g+col]="B";
            }
        }

    }
    else{
        goto AirCarrier;
    }


}//end Of BattleShip.
else if(i==2){   //PlaceMent of Cruiser Ship.
    if(direction == 1 && row <=12){
        for(int r=0;r<3;r++){
            if(user15[r+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                user15[t+row][col]="C";
            }
        }

    }
    else if(direction==0 && col<=12){

     for(int r=0;r<3;r++){
            if(user15[row][r+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                user15[row][t+col]="C";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}
//end Of Cruiser Ship.
else if(i==3){   //Submarice Placement
    if(direction == 1 && row <=12){
        for(int w=0;w<3;w++){
            if(user15[w+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                user15[q+row][col]="S";
            }
        }

    }
    else if(direction==0 && col<=12){

     for(int w=0;w<3;w++){
            if(user15[row][w+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                user15[row][q+col]="S";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Submarine
else if(ShipSize[i]==2){   //PlaceMent of Destroyer
    if(direction == 1 && row <=13){
        for(int m=0;m<2;m++){
            if(user15[m+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                user15[n+row][col]="D";
            }
        }

    }
    else if(direction==0 && col<=13){

     for(int m=0;m<2;m++){
            if(user15[row][m+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                user15[row][n+col]="D";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Destroyer Ship.

}
cout << "Ships of your 15x15 Grid Has been Placed Successfully!" << endl << endl;
for (int x = 0; x < 16; x++) {
for (int y = 0; y < 16; y++) {
           if (y>=10 && x!=0){
                cout << user15[x][y] << "  ";
}
else
            cout  << user15[x][y] << " ";

}
cout << endl;

}
ofstream userof15("user15.txt");
for (int x = 0; x < 16; x++) {
for (int y = 0; y < 16; y++) {
           if (y>=10 && x!=0){
                userof15 << user15[x][y] << "  ";
}
else
            userof15 << user15[x][y] << " ";

}
userof15 << endl;

}

}
void UserShip20(){
    int row,col;
    int direction;
for (int i = 0;i<size;i++){
Sleep(500);
srand(time(0));
direction = rand()%2; //1 for Vertical Positioning and 0 for Horizontal Positioning.
AirCarrier:
row = (rand()%20)+1;
col = (rand()%20)+1;
int counter=0;
if(ShipSize[i]==5){ //Placement of Air Carrier.
    if(direction == 1 && row<=15){
    for(int j = row;j<row+5;j++){
        for(int k = col;k<=col;k++){
            user20[j][k]="A";
        }
    }
    }
    else if (direction==0 && col<=15){
        for (int j = row;j<=row;j++){
            for(int k = col;k<col+5;k++){
                user20[j][k]="A";
            }
        }
    }
    else
        goto AirCarrier;
} //End of Air Carrier
else if(ShipSize[i]==4){   //PlaceMent of BattleShip.
    if(direction == 1 && row <=16){
        for(int a=0;a<4;a++){
            if(user20[a+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                user20[g+row][col]="B";
            }
        }

    }
    else if(direction==0 && col<=16){

     for(int a=0;a<4;a++){
            if(user20[row][a+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 4){
            for(int g=0;g<4;g++){
                user20[row][g+col]="B";
            }
        }

    }
    else{
        goto AirCarrier;
    }


}//end Of BattleShip.
else if(i==2){   //PlaceMent of Cruiser Ship.
    if(direction == 1 && row <=17){
        for(int r=0;r<3;r++){
            if(user20[r+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                user20[t+row][col]="C";
            }
        }

    }
    else if(direction==0 && col<=17){

     for(int r=0;r<3;r++){
            if(user20[row][r+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int t=0;t<3;t++){
                user20[row][t+col]="C";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}
//end Of Cruiser Ship.
else if(i==3){   //Submarice Placement
    if(direction == 1 && row <=17){
        for(int w=0;w<3;w++){
            if(user20[w+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                user20[q+row][col]="S";
            }
        }

    }
    else if(direction==0 && col<=17){

     for(int w=0;w<3;w++){
            if(user20[row][w+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 3){
            for(int q=0;q<3;q++){
                user20[row][q+col]="S";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Submarine
else if(ShipSize[i]==2){   //PlaceMent of Destroyer
    if(direction == 1 && row <=18){
        for(int m=0;m<2;m++){
            if(user20[m+row][col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                user20[n+row][col]="D";
            }
        }

    }
    else if(direction==0 && col<=18){

     for(int m=0;m<2;m++){
            if(user20[row][m+col]=="o"){
                ++counter;
            }
        else{
            goto AirCarrier;
        }

        }
        if(counter == 2){
            for(int n=0;n<2;n++){
                user20[row][n+col]="D";
            }
        }

    }
    else{
        goto AirCarrier;
    }



}//end Of Destroyer Ship.

}
cout << "Ships of your 20x20 Grid Has been Placed Successfully!" << endl << endl;
for (int x = 0; x < 21; x++) {
for (int y = 0; y < 21; y++) {
           if (y>=10 && x!=0){
                cout << user20[x][y] << "  ";
}
else
            cout  << user20[x][y] << " ";

}
cout << endl;

}
ofstream userof20("user20.txt");
for (int x = 0; x < 21; x++) {
for (int y = 0; y < 21; y++) {
           if (y>=10 && x!=0){
                userof20 << user20[x][y] << "  ";
}
else
            userof20 << user20[x][y] << " ";

}
userof20 << endl;

}

}

DisplayMainCompBoard(){ //Displaying Computer 10x10 Grid After Attacking

for (int i=0;i < 11 ; i ++ ){
     for ( int j=0; j <11 ; j++ ){
         cout <<   array[i][j]  << " ";
     }
     cout << endl;
      }
 }
int TargetsysForComp10( int& Totalhit_U ,  int& x , int& y ,ifstream &Compboard10) { //Missile Target System on 10x10 Computer Board by User

    string read[11][11];






    for ( int i = 0 ; i < 11 ; i++  ) {
      for ( int j = 0 ; j < 11 ; j++) {
          Compboard10 >> read[i][j];

          if (i==x && j==y ) {
            if (read[i][j]=="S" || read[i][j]=="A" || read[i][j]=="D" || read[i][j]=="C" || read[i][j]== "B" ) {
                ++Totalhit_U;
                array[i][j]="H";
                sndPlaySound("ghori.wav",SND_ASYNC);


             }  else if ( read[i][j]=="o"  ) {
                array[i][j]="M";
                sndPlaySound("noob.wav",SND_ASYNC);
             }
          }

      }
    }
   Compboard10.close();
    return Totalhit_U;
}
int TargetsysForUser10(int& Totalhit_C,int& x,int& y,ifstream& Userboard10){ //Missile Target System on 10x10 User Board by Computer
Sleep(2500);
 string read[11][11];
    for ( int i = 0 ; i < 11 ; i++  ) {
      for ( int j = 0 ; j < 11 ; j++) {
          Userboard10 >> read[i][j];

          if (i==x && j==y ) {
            if (read[i][j]=="S" || read[i][j]=="A" || read[i][j]=="D" || read[i][j]=="C" || read[i][j]== "B" ) {
                ++Totalhit_C;
                user10[i][j]="H";
                sndPlaySound("ghori.wav",SND_ASYNC);

             }  else if ( read[i][j]=="o"  ) {
                user10[i][j]="M";
                sndPlaySound("miss.wav",SND_ASYNC);
             }
          }

      }
    }

   Userboard10.close();
    return Totalhit_C;
 }
void DisplayUser10x10Board(){ //Displaying User 10x10 Board after the Attacks has been Done by Computer!
for (int x = 0; x < 11; x++) {
for (int y = 0; y < 11; y++) {
  cout  << user10[x][y] << " ";
}
cout << endl;
}
}
int RandomXgen(){ //Random Row Generator for Computer To target on User's 10x10 Board.
srand(time(NULL));
int x = rand()%10+1;
return x;
}
int RandomYgen(){ //Random Column Generator for Computer To target on User's 10x10 Board.
srand(time(NULL));
int y = rand()%10+1;
return y;
}
void TargetSystemFor10x10(){ //Main System for Missile Launching on 10x10 Grid By User and Computer!
DisplayMainCompBoard();
int Totalhit_U=0;
int Missilehit_U=0;
int Totalhit_C=0;
int Missilehit_C=0;
// file exists already:
ifstream Compboard10("random10.txt");
ifstream Userboard10("User10.txt");
char letter;
int number=0;
int abcissa=0;
int ordinate=0;
int PCabcissa=0;
int PCordinate=0;
int controller_U=0;
int controller_PC=0;
int counter=0;
int Missed_U = 0;
int Missed_C = 0;
    do {
            Sleep(3000);
       sndPlaySound("Mario.wav",SND_ASYNC);
       ChangeAbcissa:

       cout << "Enter the x- address : (A~J) : ";
       cin >> letter;
       if ((int)letter >= 65 && (int)letter <= 74 ) {
          goto
          ChangeOrdinate;
       }  else {
           cout << "Wrong Abcissa: input again!" << endl;
           goto
           ChangeAbcissa;
       }
       ChangeOrdinate:
       cout << "Enter the y address : (0~9) : ";
       cin >> number;
       if(number<0 || number>=10){
        cout << "Input the Number According to the Board!"<<endl<<endl;
        goto
        ChangeOrdinate;
       }
       if (number >=0 && number <=9 ) {
            if  (UserCheckX== (int)letter && UserCheckY==number)  {
           cout << "~~~~~~~~~~~~~~~~~~~***************~~~~~~~~~~~~~~~~~~~~~~" << endl;
           cout << "-----------Pick a Better Location! Duh!-----------------" << endl;
           cout << "~~~~~~~~~~~~~~~~~~~***************~~~~~~~~~~~~~~~~~~~~~~" << endl;
           goto
           ChangeAbcissa;
           }
       }
       UserCheckX= (int)letter;
       UserCheckY=number;
            abcissa= ( (int)letter ) - 64;
            ordinate= number+1;
            cout << "x_Coordinate= " << abcissa<< endl;
            cout << "y_Coordinate= " << ordinate << endl;
            if (Totalhit_U!=0 || controller_U>0){ //This "If" Condition enables to Open and Read the File Properly!
           Compboard10.open("random10.txt");
            }
            ++controller_U;
           Missilehit_U = TargetsysForComp10( Totalhit_U, abcissa, ordinate,Compboard10);
           cout << "Displaying Computer Board after being attack by You: "<<endl;

        DisplayMainCompBoard();
        Sleep(200);

        RandomGen:
            PCabcissa = RandomXgen();
            Sleep(500);
            PCordinate = RandomYgen();
            if (ComputerCheckX==PCabcissa && ComputerCheckY==PCordinate){
            goto
            RandomGen;
            }
            if (Totalhit_C!=0 || controller_PC>0){ //This "If" Condition enables to Open and Read the File Properly!
           Userboard10.open("user10.txt");
            }
            ++controller_PC;
            Missilehit_C = TargetsysForUser10( Totalhit_C, PCabcissa, PCordinate,Userboard10);
            cout << "Displaying Your Board after being attack by PC: "<<endl;

            DisplayUser10x10Board();
            ++counter;
           Missed_U = counter - Missilehit_U;
           Missed_C = counter - Missilehit_C;
            cout << "User Score Right now is : " << (double)Missilehit_U - ((double)Missed_U*(0.25)) << endl;
            cout << "Computer Score Right now is : " << (double)Missilehit_C - ((double)Missed_C*(0.25)) << endl;


     } while (Missilehit_U <= 16 || Missilehit_C == 16 );
       if(Missilehit_C == 17){
        cout << "Computer Won! You Lose"<< endl;

       }
        else if (Missilehit_U == 17){
            cout << "You have won the Game"<< endl;
        }

    }
DisplayMainCompBoard15(){ //Displaying Computer 15x15 Grid After Attacking

for (int x = 0; x < 16; x++) {
for (int y = 0; y < 16; y++) {
           if (y>=10 && x!=0){
                cout << array_15[x][y] << "  ";
}
else
            cout << array_15[x][y] << " ";

}
cout << endl;

}
 }
int TargetsysForComp15( int& Totalhit_U ,  int& x , int& y ,ifstream &Compboard15) { //Missile Target System on 15x15 Computer Board by User

    string read[16][16];






    for ( int i = 0 ; i < 16 ; i++  ) {
      for ( int j = 0 ; j < 16 ; j++) {
          Compboard15 >> read[i][j];

          if (i==x && j==y ) {
            if (read[i][j]=="S" || read[i][j]=="A" || read[i][j]=="D" || read[i][j]=="C" || read[i][j]== "B" ) {
                ++Totalhit_U;
                array_15[i][j]="H";
                sndPlaySound("ghori.wav",SND_ASYNC);


             }  else if ( read[i][j]=="o"  ) {
                array_15[i][j]="M";
                sndPlaySound("noob.wav",SND_ASYNC);
             }
          }

      }
    }
   Compboard15.close();
    return Totalhit_U;
}
int TargetsysForUser15(int& Totalhit_C,int& x,int& y,ifstream& Userboard15){ //Missile Target System on User 15x15 Board by Computer
Sleep(2500);
 string read[16][16];
    for ( int i = 0 ; i < 16 ; i++  ) {
      for ( int j = 0 ; j < 16 ; j++) {
          Userboard15 >> read[i][j];

          if (i==x && j==y ) {
            if (read[i][j]=="S" || read[i][j]=="A" || read[i][j]=="D" || read[i][j]=="C" || read[i][j]== "B" ) {
                ++Totalhit_C;
                user15[i][j]="H";
                sndPlaySound("ghori.wav",SND_ASYNC);

             }  else if ( read[i][j]=="o"  ) {
                user15[i][j]="M";
                sndPlaySound("miss.wav",SND_ASYNC);
             }
          }

      }
    }

   Userboard15.close();
    return Totalhit_C;
 }
void DisplayUser15x15Board(){ //Displaying User 15x15 Board after the Attacks has been Done By Computer!
for (int x = 0; x < 16; x++) {
for (int y = 0; y < 16; y++) {
           if (y>=10 && x!=0){
                cout << user15[x][y] << "  ";
}
else
            cout << user15[x][y] << " ";

}
cout << endl;
}
}
int RandomXgen15(){ //Random Row Generator for Computer To target on User's 15x15 Board.
srand(time(NULL));
int x = rand()%15+1;
return x;
}
int RandomYgen15(){ //Random Column Generator for Computer To target on User's 15x15 Board.
srand(time(NULL));
int y = rand()%15+1;
return y;
}
void TargetSystemFor15x15(){ //Main System for Missile Launching on 15x15 Grid By User and Computer!
DisplayMainCompBoard15();
int Totalhit_U=0;
int Missilehit_U=0;
int Totalhit_C=0;
int Missilehit_C=0;
// file exists already:
ifstream Compboard15("random15.txt");
ifstream Userboard15("User15.txt");
char letter;
int number=0;
int abcissa=0;
int ordinate=0;
int PCabcissa=0;
int PCordinate=0;
int controller_U=0;
int controller_PC=0;
int counter=0;
int Missed_U = 0;
int Missed_C = 0;
    do {
            Sleep(3000);
sndPlaySound("Mario.wav",SND_ASYNC);
       ChangeAbcissa:

       cout << "Enter the x- address : (A~J) : ";
       cin >> letter;
       if ((int)letter >= 65 && (int)letter <= 79 ) {
          goto
          ChangeOrdinate;
       }  else {
           cout << "Wrong Abcissa: input again!" << endl;
           goto
           ChangeAbcissa;
       }
       ChangeOrdinate:
       cout << "Enter the y address : (0~14) : ";
       cin >> number;
       if(number<0 || number>=15){
        cout << "Input the Number According to the Board!"<<endl<<endl;
        goto
        ChangeOrdinate;
       }
       if (number >=0 && number <=14 ) {
            if  (UserCheckX== (int)letter && UserCheckY==number)  {
           cout << "~~~~~~~~~~~~~~~~~~~***************~~~~~~~~~~~~~~~~~~~~~~" << endl;
           cout << "-----------Pick a Better Location! Duh!-----------------" << endl;
           cout << "~~~~~~~~~~~~~~~~~~~***************~~~~~~~~~~~~~~~~~~~~~~" << endl;
           goto
           ChangeAbcissa;
           }
       }
       UserCheckX= (int)letter;
       UserCheckY=number;
            abcissa= ( (int)letter ) - 64;
            ordinate= number+1;
            cout << "x_Coordinate= " << abcissa<< endl;
            cout << "y_Coordinate= " << ordinate << endl;
            if (Totalhit_U!=0 || controller_U>0){ //This "If" Condition enables to Open and Read the File Properly!
           Compboard15.open("random15.txt");
            }
            ++controller_U;
           Missilehit_U = TargetsysForComp15( Totalhit_U, abcissa, ordinate,Compboard15);
           cout << "Displaying Computer Board after being attack by You: "<<endl;
        DisplayMainCompBoard15();
        Sleep(200);

        RandomGen:
            PCabcissa = RandomXgen15();
            Sleep(500);
            PCordinate = RandomYgen15();
            if (ComputerCheckX==PCabcissa && ComputerCheckY==PCordinate){
            goto
            RandomGen;
            }
            if (Totalhit_C!=0 || controller_PC>0){ //This "If" Condition enables to Open and Read the File Properly!
           Userboard15.open("user15.txt");
            }
            ++controller_PC;
            Missilehit_C = TargetsysForUser15( Totalhit_C, PCabcissa, PCordinate,Userboard15);
            cout << "Displaying Your Board after being attack by PC: "<<endl;
            DisplayUser15x15Board();
            ++counter;
           Missed_U = counter - Missilehit_U;
           Missed_C = counter - Missilehit_C;
            cout << "User Score Right now is : " << (double)Missilehit_U - ((double)Missed_U*(0.25)) << endl;
            cout << "Computer Score Right now is : " << (double)Missilehit_C - ((double)Missed_C*(0.25)) << endl;


     } while (Missilehit_U <= 16 || Missilehit_C == 16 );
       if(Missilehit_C == 17){
        cout << "Computer Won! You Lose"<< endl;
       }
        else if (Missilehit_U == 17){
            cout << "You have won the Game"<< endl;
        }

    }
DisplayMainCompBoard20(){ //Displaying Computer 20x20 Grid After Attacking

for (int x = 0; x < 21; x++) {
for (int y = 0; y < 21; y++) {
           if (y>=10 && x!=0){
                cout << array_20[x][y] << "  ";
}
else
            cout << array_20[x][y] << " ";

}
cout << endl;

}
 }
int TargetsysForComp20( int& Totalhit_U ,  int& x , int& y ,ifstream &Compboard20) { //Missile Target System on 20x20 Computer Board by User

    string read[21][21];






    for ( int i = 0 ; i < 21 ; i++  ) {
      for ( int j = 0 ; j < 21 ; j++) {
          Compboard20 >> read[i][j];

          if (i==x && j==y ) {
            if (read[i][j]=="S" || read[i][j]=="A" || read[i][j]=="D" || read[i][j]=="C" || read[i][j]== "B" ) {
                ++Totalhit_U;
                array_20[i][j]="H";
                sndPlaySound("uhhhh.wav",SND_ASYNC);
                 }
          else if ( read[i][j]=="o" ) {
                array_20[i][j]="M";
                sndPlaySound("noob.wav",SND_ASYNC);
             }
          }

      }
    }
   Compboard20.close();
    return Totalhit_U;
}
int TargetsysForUser20(int& Totalhit_C,int& x,int& y,ifstream& Userboard20){ //Missile Target System on 20x20 User Board by Computer
Sleep(2500);
 string read[21][21];
    for ( int i = 0 ; i < 21; i++  ) {
      for ( int j = 0 ; j < 21 ; j++) {
          Userboard20 >> read[i][j];

          if (i==x && j==y ) {
            if (read[i][j]=="S" || read[i][j]=="A" || read[i][j]=="D" || read[i][j]=="C" || read[i][j]== "B" ) {
                ++Totalhit_C;
                user20[i][j]="H";
                sndPlaySound("ghori.wav",SND_ASYNC);

             }  else if ( read[i][j]=="o"  ) {
                user20[i][j]="M";
                sndPlaySound("miss.wav",SND_ASYNC);
             }
          }

      }
    }

   Userboard20.close();
    return Totalhit_C;
 }
void DisplayUser20x20Board(){ //Displaying User 20x20 Board after the Attacks has been Done By Computer!
for (int x = 0; x < 21; x++) {
for (int y = 0; y < 21; y++) {
           if (y>=10 && x!=0){
                cout << user20[x][y] << "  ";
}
else
            cout << user20[x][y] << " ";

}
cout << endl;
}
}
int RandomXgen20(){ //Random Row Generator for Computer To target on User's 20x20 Board.
srand(time(NULL));
int x = rand()%20+1;
return x;
}
int RandomYgen20(){ //Random Column Generator for Computer To target on User's 20x20 Board.
srand(time(NULL));
int y = rand()%20+1;
return y;
}
void TargetSystemFor20x20(){ //Main System for Missile Launching on 20x20 Grid By User and Computer!
DisplayMainCompBoard20();
int Totalhit_U=0;
int Missilehit_U=0;
int Totalhit_C=0;
int Missilehit_C=0;
// file exists already:
ifstream Compboard20("random20.txt");
ifstream Userboard20("User20.txt");
char letter;
int number=0;
int abcissa=0;
int ordinate=0;
int PCabcissa=0;
int PCordinate=0;
int controller_U=0;
int controller_PC=0;
int counter=0;
int Missed_U = 0;
int Missed_C = 0;
    do {
            Sleep(3000);
          sndPlaySound("Mario.wav",SND_ASYNC);
       ChangeAbcissa:

       cout << "Enter the x- address : (A~J) : ";
       cin >> letter;
       if ((int)letter >= 65 && (int)letter <= 84 ) {
          goto
          ChangeOrdinate;
       }  else {
           cout << "Wrong Abcissa: input again!" << endl;
           goto
           ChangeAbcissa;
       }
       ChangeOrdinate:
       cout << "Enter the y address : (0~19) : ";
       cin >> number;
       if(number<0 || number>=20){
        cout << "Input the Number According to the Board!"<<endl<<endl;
        goto
        ChangeOrdinate;
       }
       if (number >=0 && number <=14 ) {
            if  (UserCheckX== (int)letter && UserCheckY==number)  {
           cout << "~~~~~~~~~~~~~~~~~~~***************~~~~~~~~~~~~~~~~~~~~~~" << endl;
           cout << "-----------Pick a Better Location! Duh!-----------------" << endl;
           cout << "~~~~~~~~~~~~~~~~~~~***************~~~~~~~~~~~~~~~~~~~~~~" << endl;
           goto
           ChangeAbcissa;
           }
       }
       UserCheckX= (int)letter;
       UserCheckY=number;
            abcissa= ( (int)letter ) - 64;
            ordinate= number+1;
            cout << "x_Coordinate= " << abcissa<< endl;
            cout << "y_Coordinate= " << ordinate << endl;
            if (Totalhit_U!=0 || controller_U>0){ //This "If" Condition enables to Open and Read the File Properly!
           Compboard20.open("random20.txt");
            }
            ++controller_U;
           Missilehit_U = TargetsysForComp20( Totalhit_U, abcissa, ordinate,Compboard20);
           cout << "Displaying Computer Board after being attack by You: "<<endl;



        DisplayMainCompBoard20();

        Sleep(200);

        RandomGen:
            PCabcissa = RandomXgen20();
            Sleep(500);
            PCordinate = RandomYgen20();
            if (ComputerCheckX==PCabcissa && ComputerCheckY==PCordinate){
            goto
            RandomGen;
            }
            if (Totalhit_C!=0 || controller_PC>0){ //This "If" Condition enables to Open and Read the File Properly!
           Userboard20.open("user20.txt");
            }
            ++controller_PC;
            Missilehit_C = TargetsysForUser20( Totalhit_C, PCabcissa, PCordinate,Userboard20);
            cout << "Displaying Your Board after being attack by PC: "<<endl;

            DisplayUser20x20Board();

            ++counter;
           Missed_U = counter - Missilehit_U;
           Missed_C = counter - Missilehit_C;
            cout << "User Score Right now is : " << (double)Missilehit_U - ((double)Missed_U*(0.25)) << endl;
            cout << "Computer Score Right now is : " << (double)Missilehit_C - ((double)Missed_C*(0.25)) << endl;


     } while (Missilehit_U <= 16 || Missilehit_C == 16 );
       if(Missilehit_C == 17){
        cout << "Computer Won! You Lose"<< endl;
       }
        else if (Missilehit_U == 17){
            cout << "You have won the Game"<< endl;
        }

    }
void Instruction(){
cout <<"\t" << "\t" <<"-------------------------------------------Instructions Of BattelShip-----------------------------"<<endl;
cout <<"\t" << "\t" << "You have to Select a Game Mode from The Following" << endl << "\t" << "\t" <<"1.Easy" <<endl<< "\t" << "\t" <<"2.Expert"<<endl << "\t" << "\t" <<"3.Hard";
cout <<"\t" << "\t" << "------->1. Your 5 Ships Will be Placed Randomly by the Game.No need to Worry About it!"<<endl;
cout <<"\t" << "\t" <<"------->2. A Gameboard will be shown on your Screen!" << endl;
cout <<"\t" << "\t" << "------->3. You have to Select the Co-ordinates of the Gameboard specified by Program to Attack a certain Position"<<endl;
cout <<"\t" << "\t" <<"------->4. Your Board Will Launch Missiles against the Specified position"<<endl;
cout <<"\t" << "\t" <<"------->5. If there will be ship at that location Then 'H' will be Printed Else 'M' will be Printed!"<<endl;
cout <<"\t" << "\t" <<"------->6. H = Hit and M=Miss"<<endl;
cout <<"\t" << "\t" <<"------->7. Whoever first Destroy all the Ships will win the game!"<<endl;
cout <<"\t" << "\t" <<"------->8. Remember! Ships are placed Either vertically or horizontally.So better use your Brain ;)"<<endl;
cout <<"\t" << "\t" <<"------->9.--------------------------------GOOD LUCK HAVE FUN! MATE---------------------------------"<<endl;

}
void Credits(){
cout << "-----------------~-~-~-~-Made by KOOKYY-~-~-~-~--------------"<<endl;

}
int main(void)
{
    int menu;

    cout << "\t" <<"\t" <<"~~~~---*-*-*--------!!!!!!!!!!!!!!!!!!!!!!!!!!!!--------*-*-*---~~~~~"<<endl;
    cout << "\t" <<"\t" <<"~~~~---*-*-*--------Welcome To Battleship--------*-*-*---~~~~~"<<endl;
    cout << "\t" <<"\t" <<"~~~~---*-*-*--------!!!!!!!!!!!!!!!!!!!!!!!!!!!!--------*-*-*---~~~~~"<<endl;
    cout << "\t" << "\t" << "Choose from the following" <<endl;
    cout << "\t" << "\t" << "Difficulty Level:" <<endl;
    cout << "\t" << "\t" << "1.Easy:" <<endl;
    cout << "\t" << "\t" << "2.Hard:" <<endl;
    cout << "\t" << "\t" << "3.Expert" <<endl;
    cout << "\t" << "\t" << "4.Instructions" <<endl;
    cout << "\t" << "\t" << "5.Credits" <<endl;
    cout << "\t" << "\t" << "6.Exit" <<endl;
    cin >> menu;
    system("cls");

switch(menu){
case 1:
Instruction();
ShowOpponentBoard(menu);
ShipsPlacement10();
Sleep(200);
UserShip10();
system("cls");
TargetSystemFor10x10();
Sleep(1000000);
break;
case 2:
    Instruction();
    ShowOpponentBoard(menu);
ShipsPlacement15();
Sleep(200);
UserShip15();
system("cls");
TargetSystemFor15x15();
Sleep(1000000);
break;
case 3:
    Instruction();
ShowOpponentBoard(menu);
ShipsPlacement20();
Sleep(200);
UserShip20();
system("cls");
TargetSystemFor20x20();
Sleep(1000000);
break;
case 4:
    Instruction();
    break;
case 5:
    Credits();
    break;
case 6:
    exit;
    break;
}
}
