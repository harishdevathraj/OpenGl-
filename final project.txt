//#include <GL/gl.h>
#include<stdio.h>
#include <GL/glut.h>
#include <math.h>
#include<string.h>
//int label;
const double PI = 3.141592654;
int night=0,stop=0,day=0;
int speed=0;
int frameNumber = 0;
int frameNumberOfCart=0;
int win1,win2;
int storeframe=0;
void circle1(GLfloat x,GLfloat y,GLfloat radius);
void display();
void keys(unsigned char key, int x, int y)
{
	if(key=='n') {
	night=1;}
	if(key=='d')
		night=0;
	if(key=='s')
		speed=(1+speed)%3;
	if(key=='r'){
	stop=1-stop;}

/*
 * Draw a cart consisting of a rectangular body and two wheels.  The wheels
 * are drawn by the drawWheel() method; a different translation is applied to each
 * wheel to move them into position under the body.  The body of the cart
 * is a red rectangle with corner at (0,-2.5), width 5, and height 2.  The
 * center of the bottom of the rectangle is at (0,0).
 */
}

void Write(double x,double y,double z,double scale,char *s)
{
int i,l=strlen(s);
glPushMatrix();
glTranslatef(x,y,z);
glScalef(scale,scale,scale);
for(i=0;i<l;i++)
glutStrokeCharacter(GLUT_STROKE_ROMAN,s[i]);
glPopMatrix();
}

void redisplay(void)
{
glClearColor(0,0,0,1);
glClear(GL_COLOR_BUFFER_BIT);
glColor3f(1.0,1.0,0.0);
Write(-0.95,0.9,1,0.0007,"Sir M Visvesvaraya Institue of Technology");
Write(-0.4,0.8,1,0.0007,"Dept. of CSE");
glColor3f(1.0,0.0,0.0);
Write(-0.75,0.4,1,0.0007,"  Graphical Implementation of ");
Write(-0.75,0.3,1,0.0007,"OpenGL Hierarchical Modeling 2D");

Write(-0.4,0.6,0.0,0.0007,"Mini Project on");
glColor3f(1.0,1.0,0.5);
Write(-0.4,-0.8,0.0,0.0006,"Press 'C' to continue");
//glColor3f(1.0,1.0,1.0);
glColor3f(1,1,0.0);
Write(-1.0,0.1,0.0,0.0007," Submitted BY:");
glColor3f(1.0,1.0,1.0);
Write(-1.0,-0.03,0.0,0.0006," Harish Devathraj: 1MV13CS038 ");
Write(-1.0,-0.2,0.0,0.0006," Gururaj: 1MV13CS037 ");
Write(-1.0,-0.4,0.0,0.0007," Under the guidance of: ");
Write(0.15,-0.415,0.0,0.0006," ELAIYARAJA P");
glFlush();
}


/*
 * This function is set as the glutTimerFunc to drive the animation
 */
void doFrame(int v) {
    frameNumber++;
	frameNumberOfCart++;
    glutPostRedisplay();
    glutTimerFunc(30,doFrame,0);
}

/*
 * This method is called from main() to initialize OpenGL.
 */
void init() {
	glClearColor(0.5f, 0.5f, 1, 1);
		// The next three lines set up the coordinates system.
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(0, 7, -1, 4, -1, 1);
	glMatrixMode(GL_MODELVIEW);
}


void keyboard1(unsigned char key ,int x ,int y)
{
if(key=='c' || key=='C')
{
glutDestroyWindow(win1);
 glutInitDisplayMode(GLUT_DOUBLE);
win2=glutCreateWindow("Windmill");
init();
   glutDisplayFunc(display);   
    glutTimerFunc(200,doFrame,0); 
	glutKeyboardFunc(keys);

}
}


void circle1(GLfloat x, GLfloat y, GLfloat radius) 
  { 
    float angle;   
    glBegin(GL_POLYGON); 
    for(int i=0;i<100;i++) 
	{ 
        angle = i*2*(PI/100); 
        glVertex2f(x+(cos(angle)*radius),y+(sin(angle)*radius)); 
    } 
    glEnd(); 
  }  




//vo
 
void drawDisk(double radius) {
	int d;
	glBegin(GL_POLYGON);
	for (d = 0; d < 32; d++) {
		double angle = 2*PI/32 * d;
		glVertex2d( radius*cos(angle), radius*sin(angle));
	}
	glEnd();
}

/*
 * Draw a wheel, centered at (0,0) and with radius 1. The wheel has 15 spokes
 * that rotate in a clockwise direction as the animation proceeds.
 */
void drawWheel() {
    int i;
	glColor3f(0,0,0);
	drawDisk(1);
	glColor3f(0.75f, 0.75f, 0.75f);
	drawDisk(0.8);
	glColor3f(0,0,0);
	drawDisk(0.2);
	glRotatef(frameNumber*20,0,0,1);
	glBegin(GL_LINES);
	for (i = 0; i < 15; i++) {
		glVertex2f(0,0);
		glVertex2d(cos(i*2*PI/15), sin(i*2*PI/15));
	}
	glEnd();
}




void drawCart() {
	glPushMatrix();
	glTranslatef(-1.5f, -0.1f, 0);
	glScalef(0.8f,0.8f,1);
	drawWheel();
	glPopMatrix();
	glPushMatrix();
	glTranslatef(1.5f, -0.1f, 0);
	glScalef(0.8f,0.8f,1);
	drawWheel();
	glPopMatrix();
	glColor3f(.1,.25,0);


	glBegin(GL_POLYGON);                // start drawing a polygon
 //glColor3f(0.5f,0.2f,0.0f);            // Set The Color To Red
  glVertex3f(-3.0f, 3.0f, 0.0f);        // Top left
  glVertex3f(1.2f, 3.0f, 0.0f);
   glColor3f(1.0f,1.5f,1.6f);
  glVertex3f(3.0f, 1.2f, 0.0f);
  
             // Set The Color To Green
  glVertex3f( 3.0f,0.0f, 0.0f);        // Bottom Right
 // glColor3f(0.0f,0.0f,1.0f);            // Set The Color To Blue
  glVertex3f(-3.0f,0.0f, 0.0f);

	
	glEnd();
	



}
void drawCart1() {
	glPushMatrix();
	glTranslatef(-1.5f, -0.1f, 0);
	glScalef(0.8f,0.8f,1);
	drawWheel();
	glPopMatrix();
	glPushMatrix();
	glTranslatef(1.5f, -0.1f, 0);
	glScalef(0.8f,0.8f,1);
	drawWheel();
	glPopMatrix();
	glColor3f(0.3,0.2,0);


	glBegin(GL_POLYGON);                // start drawing a polygon

	glVertex2f(-2.5f,0);
	glVertex2f(2.5f,0);
	glColor3f(1,0.2,0);
	glVertex2f(2.5f,2);
	glVertex2f(-2.5f,2);
	

	
	glEnd();
	



}

/*
 * Draw a sun with radius 0.5 centered at (0,0).  There are also 13 rays which
 * extend outside from the sun for another 0.25 units.
 */
void drawSun() {
	int i;
	
		glColor3f(1,1,0);
		for (i = 0; i < 13; i++) { // Draw 13 rays, with different rotations.
			glRotatef( 360 / 13, 0, 0, 1 ); // Note that the rotations accumulate!
			glBegin(GL_LINES);
			glVertex2f(0, 0);
			glVertex2f(0.75f, 0);
			glEnd();
		}
	
	drawDisk(0.5);
//else{
//glColor3f(1,1,1);
		
//	}drawDisk(0.5);
	
//	glColor3f(0,0,0);
}

void drawSun1() {
	
	if(night==1){

	               glColor3f(1.0,1.0,1.0);
				   drawDisk(0.35);}
				  // glColor3f(1.0,1.0,1.0);
				  // circle(0.9);
				  // glFlush();
		//		   glutSwapBuffers();
		
		
		//drawDisk(0.5);
	
	//drawDisk(0.5);
}
void drawSun2() {
	
	if(night==1){

	               glColor3f(0.0,0.0,0.0);
				   drawDisk(0.35);}
				  // glColor3f(1.0,1.0,1.0);
				  // circle(0.9);
				  // glFlush();
		//		   glutSwapBuffers();
		
		
		//drawDisk(0.5);
	
	//drawDisk(0.5);
}
/*
 * Draw a windmill, consisting of a pole and three vanes.  The pole extends from the
 * point (0,0) to (0,3).  The vanes radiate out from (0,3).  A rotation that depends
 * on the frame number is applied to the whole set of vanes, which causes the windmill
 * to rotate as the animation proceeds.  Note that this method changes the current
 * transform in the GL context gl!  The caller of this subroutine should take care
 * to save and restore the original transform, if necessary.
 */
void drawWindmill() {
	int i;
	glColor3f(0.8f, 0.8f, 0.9f);
	glBegin(GL_POLYGON);
	glVertex2f(-0.05f, 0);    //thick ness of the windmill pole
	glVertex2f(0.05f, 0);
	glVertex2f(0.05f, 3);
	glVertex2f(-0.05f, 3);
	glEnd();
	glTranslatef(0, 3, 0);
	glRotated(frameNumber * (180.0/(10*(5*speed+4))), 0, 0, 1);
	glColor3f(0.4f, 0.4f, 0.8f);
	for (i = 0; i < 3; i++) {
		glRotated(120, 0, 0, 3);  // Note: These rotations accumulate.
		glBegin(GL_POLYGON);
		glVertex2f(0,0);
		glVertex2f(0.5f, 0.1f);
		glVertex2f(1.5f,0);
		glVertex2f(0.5f, -0.1f);
		glEnd();
	}
}

/*
 * This function is called when the image needs to be redrawn.
 * It is installed by main() as the GLUT display function.
 * It draws the current frame of the animation.
 */
void display() {
	

	glClear(GL_COLOR_BUFFER_BIT); // Fills the scene with blue.
	glLoadIdentity();
	if(night==1){
		glClearColor(0, 0, 0, 1);
		
		glColor3f(1.0,1.0,1.0);
    circle1(1.87,2.85,0.01);
	circle1(1.9,2.65,0.01);
	circle1(1.56,3.5,0.02);

	circle1(0.85,3.5,0.01);
	circle1(1.345,2.5,0.01);
	circle1(2.02,2.69,0.01);
	circle1(1.8,3.75,0.02);
	circle1(0.99,3.45,0.01);
	circle1(1.345,2.5,0.01);
	circle1(7.40,2.8,0.01);
	circle1(6.120,2.5,0.01);
	circle1(4.90,7.5,0.01);
	circle1(8.0,3.5,0.01);
	circle1(6.40,3.5,0.01);
	circle1(4.55,3.5,0.01);
	circle1(7.65,3.5,0.01);

	circle1(8.23,3.1,0.01);
	circle1(6.2,2.5,0.01);
	circle1(4.95,2.85,0.01);
	circle1(6.15,2.75,0.01);

	


	}
	else 
		glClearColor(0.4,0.7,1.0,1);
	if(night==1)
	/* Draw three green triangles to form a ridge of hills in the background */
	glColor3f(0,0.2f,0.0f);
	else 
		
	
	

		glColor3f(0, 0.6f, 0.2f);
	glBegin(GL_POLYGON);
	glVertex2f(-3,-1);
	glVertex2f(1.5f,1.65f);
	glVertex2f(5,-1);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex2f(-3,-1);
	glVertex2f(3,2.1f);
	glVertex2f(7,-1);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex2f(0,-1);
	glVertex2f(6,1.2f);
	glVertex2f(20,-1);
	glEnd();
	

	/* Draw a bluish-gray rectangle to represent the road. */
	if(night==0)
	glColor3f(0.4f, 0.4f, 0.5f);
	else
		glColor3f(0.3f,0.3f,0.4f);
	glBegin(GL_POLYGON);
	glVertex2f(0,-0.4f);
	glVertex2f(7,-0.4f);
	glVertex2f(7,0.4f);
	glVertex2f(0,0.4f);
	glEnd();

	/* Draw a white line to represent the stripe down the middle
	 * of the road. */

	glLineWidth(4);
	// Set the line width to be 6 pixels.
	if(night==1) glColor3f(0.9,0.9,0.9);
	else
		glColor3f(1,1,1);



	glBegin(GL_LINES);
	glVertex2f(0,0);
	glVertex2f(0.5,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(0.75,0);
	glVertex2f(1.25,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(1.5,0);
	glVertex2f(2.0,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(2.25,0);
	glVertex2f(2.75,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(3.0,0);
	glVertex2f(3.5,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(3.75,0);
	glVertex2f(4.25,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(4.5,0);
	glVertex2f(5.0,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(5.25,0);
	glVertex2f(5.75,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(6.0,0);
	glVertex2f(6.5,0);
	glEnd();

	glBegin(GL_LINES);
	glVertex2f(6.75,0);
	glVertex2f(7.25,0);
	glEnd();
	glBegin(GL_LINES);
	glVertex2f(7.5,0);
	glVertex2f(8.0,0);
	glEnd();

	glColor3f(1,1,1);
	glBegin(GL_LINES);
	glVertex2f(0,0.33);
	glVertex2f(7,0.33);
	glEnd();

	glColor3f(1,1,1);
	glBegin(GL_LINES);
	glVertex2f(0,-0.33);
	glVertex2f(7,0-0.33);
	glEnd();
	glLineWidth(1);  // Reset the line width to be 1 pixel.

	/* Draw the sun.  The drawSun method draws the sun centered at (0,0).  A 2D translation
	 * is applied to move the center of the sun to (5,3.3).   A rotation makes it rotate*/

	glPushMatrix();
	if(night==0)
		glTranslated(5.8,3,0);
	else
		glTranslated(100.8,300,0);
	//glRotated(-frameNumber*0.7,0,0,1);
	drawSun();
	glPopMatrix();

	glPushMatrix();
		glTranslated(2.8,3.5,0);
		drawSun1();
		glPopMatrix();

		glPushMatrix();
		glTranslated(2.75,3.68,0);
		drawSun2();
		glPopMatrix();

		if(night==0)
			glColor3f(0.5,0.5,0.5);
		else
			glColor3f(0.1,0.1,0.1);

	circle1(1.6,3.13,.200);
	circle1(1.75,3.23,.300);
	circle1(1.1,3.28,.400);
    circle1(1.5,3.33,.300);

	/* Draw three windmills.  The drawWindmill method draws the windmill with its base 
	 * at (0,0), and the top of the pole at (0,3).  Each windmill is first scaled to change
	 * its size and then translated to move its base to a different paint.  In the animation,
	 * the vanes of the windmill rotate.  That rotation is done with a transform inside the
	 * drawWindmill method. */

	glPushMatrix();
	glTranslated(0.75,1,0);
	glScaled(0.6,0.6,1);
	drawWindmill();
	glPopMatrix();

	glPushMatrix();
	glTranslated(2.2,1.6,0);
	glScaled(0.4,0.4,1);
	drawWindmill();
	glPopMatrix();

	glPushMatrix();
	glTranslated(5.7,0.8,0);
	glScaled(0.7,0.7,1);
	drawWindmill();
	glPopMatrix();

	/* Draw the cart.  The drawCart method draws the cart with the center of its base at
	 * (0,0).  The body of the cart is 5 units long and 2 units high.  A scale is first
	 * applied to the cart to make its size more reasonable for the picture.  Then a
	 * translation is applied to move the cart horizontally.  The amount of the translation
	 * depends on the frame number, which makes the cart move from left to right across
	 * the screen as the animation progresses.  The cart animation repeats every 300 
	 * frames.  At the beginning of the animation, the cart is off the left edge of the
	 * screen. */

	glPushMatrix();
	if(stop==0){
		glTranslated(-3 + 13*(frameNumberOfCart % 500) / 300.0, 0, 0);
		storeframe=frameNumberOfCart;
		//printf("%d\n",frameNumberOfCart);
	}
	else{
		glTranslated(-3 + 13*(storeframe % 500) / 300.0, 0, 0);
		frameNumberOfCart=storeframe;
	}
	glScaled(0.22,0.22,1);
	drawCart();
	glPopMatrix();
		



	glPushMatrix();
	glTranslated(-3 + 13*(frameNumber % 300) / 200.0, 0, 0);
	glScaled(0.3,0.3,1);
	drawCart1();
	glPopMatrix();
	

	
	//glutSwapBuffers();

	glFlush();
	glutSwapBuffers();

}  // end display




void main(int argc, char** argv) {
    glutInit(&argc, argv); 
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);

    glutInitWindowSize(700,500);
    glutInitWindowPosition(100,100);  
	win1=glutCreateWindow("INTRODUCTION"); 
    //glutCreateWindow("A Scenic View of Windmill"); 

   // init();

    glutDisplayFunc(redisplay);   
   // glutTimerFunc(200,doFrame,0); 
	glutKeyboardFunc(keyboard1);

    glutMainLoop(); 
    //return 0;
}    


