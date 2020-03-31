# challenge4
// Created on Mon March 30 2020
int l_motor = 0;
int r_motor = 2;
int speed = 50; 
int slow = 20;
int target = 250;
int pause = 300;
int right_range = 2;
int left_range = 0;
int middle_range = 1;
int black_line = 800;
int tophat = 5;
int tophat_2 = 6;


void forwards() { // go forward
   motor(l_motor,speed);  
   motor(r_motor,speed);
}

void backwards() { // go backwards
   motor(l_motor,-speed);  
   motor(r_motor,-speed);
}


void turn_right() {
   motor(l_motor,speed); // turn right
   motor(r_motor,-speed);
}

void turn_left() { // turn left  
   motor(l_motor,-speed);
   motor(r_motor,speed);
   msleep(600);
   forwards();
   msleep(1500);
   ao();   
}


void veer_left() {
	 motor(r_motor,speed);
	 motor(l_motor,slow);
}

void veer_right() {
   motor(r_motor,slow);
	 motor(l_motor,speed);
}

void findline() {
while(analog (tophat) < target) { // go foward until it sees the black line
       forwards();
       }
       ao(); 
       printf("found line!\n"); 
}

void followline(){
while (analog(middle_range) > target) { // follow the line until it sees the wall
        printf("starting line follow!\n");
 if (analog(tophat) > black_target){ // stay on the line
        veer_left();
        printf("vearing left!\n");
        } 
  
 if (analog(tophat) < black_line) { // stay on the line
        veer_right();
        printf("vearing right!\n");
        }
        }
	    ao();
	
}

void wallrun() {
while(analog(left_range) >= target) { 
    
 if (analog(right_range) <= target) { 
        veer_left(); //veering left 
        printf("veer away!/n");// makes the robot veer away left on the screen
        }

 if (analog(right_range) >= target) {
        veer_right(); // veer right
        printf("veer toward wall!/n"); // veer towards the wall
        }
 
}

void followline2() {
while (analog(tophat_2) < target) { // follow the line until it finds the wall
        printf("starting line follow!\n");
 if (analog(tophat) > black_line) { // stay on the line
        veer_left();
        printf("vearing left!\n");
 }
  
 if (analog(tophat) < black_line) { // stay on the line
        veer_right();
        printf("vearing right!\n");
 }
 }
 ao();
	
}

int main() {	
	
turn_left();
msleep(400);
findline();
followline();
backwards();
turn_left();
msleep(600);
findline();
followline2();
}
