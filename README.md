Menu-And-Submenu--Open-GL--CS7
==============================

By: Novice Dalasamooth khamphadith FNSC 0380
    Mr Souksavath manibod FNSC 0032
    Miss Nid Phunthavong FNSc 0036
      Class Cs7  Year 4




#include <GL/glut.h>
int shape;
int color;

void init(void)
{
  glEnable(GL_DEPTH_TEST);
	glClearColor(0.5, 0.5, 0.5, 0.0);	// ຕັ້ງ​ຄ່າການ​ສະ​ແດງ​ຜົນ​ທາງ​ໜ້າ​ຈໍ​ເປັນ​ສີ​ຂີ້​ເທົາ​ຈ່າງໆ
	glColor3f(1.0, 1.0, 1.0);	
	glMatrixMode(GL_PROJECTION);	
	glRotatef (30.0, 0.0, 1.0, 1.0);
      glOrtho(-50,50,-50,50,-50,50);
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();
}

void mainMenu (int option)
{
	switch (option) 
	{
		case 1: glClearColor (1.0, 1.0, 1.0, 0.0);  
			break;	// ​ຂຽນ​ພື້ນຫຼັງ​ສີ​ເປັນຂາວ
		case 2: glClearColor (1.0, 1.0, 0.0, 0.0);  
			break;	// ຂຽນ​ພື້ນຫຼັງ​ເປັນສີເຫຼືອງ
		case 3: glClearColor(0.0, 1.0, 1.0, 1.0);
			break; //ຂຽນ​ພື້ນຫຼັງ​ເປັນສີ
	}
	glutPostRedisplay ( );
}

void colorFcn (int item)
{
	color = item;
	glutPostRedisplay();
}

void shapeFcn (int item)
{
	shape = item;
	glutPostRedisplay();
}

void display (void)
{
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);	// ລົບ​ລ້າງ​ການ​ສະ​ແດງ​ຜົນ​ທາງ​ໜ້າ​ຈໍ.
	
	glEnable (GL_LINE_SMOOTH);
	glEnable (GL_BLEND);
	glBlendFunc (GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);

	switch (color)
	{
		case 1: glColor3f (1.0, 0.0, 0.0);	 
			break;	// ປ່ຽນ​ສີ​ເປັນ​ສີ​ແດງ
		case 2: glColor3f (0.0, 1.0, 0.0);	 
			break;	// ປ່ຽນ​ສີ​ເປັນ​ສີ​ຂຽວ
		case 3: glColor3f (0.0, 0.0, 1.0);	 
			break;	// ປ່ຽນ​ສີ​ເປັນ​ສີຟ້າ
		case 4: glColor3f (0.0, 0.0, 0.0);	 
			break;	// ປ່ຽນ​ສີ​ເປັນ​ສີດຳ
	}

	switch (shape)
	{
		case 1 : glutWireTorus (5, 20, 10, 10); 
			break;	// ແຕ້ມ​ຮູບ Torus
		case 2 : glutWireSphere (30, 50, 20);  
			break; // ແຕ້ມ​ຮູບ Sphere
		case 3 : glutWireTeapot (25);	 
			break;	// ​ແຕ້ມ​ຮູບ​ Teapot
	}

	glutSwapBuffers();
	glFlush ( );     
}

void main (int argc, char **argv)
{
	GLint subMenu1, subMenu2;			// ປະ​ກາດ​ຕົວ​ແປ​ໃນ​ການ​ສ້າງ Menu.
	glutInit (&argc, argv);
	glutInitDisplayMode (GLUT_SINGLE | GLUT_RGB);
	glutInitWindowPosition (50, 50);
	glutInitWindowSize (500, 500);
	glutCreateWindow ("Menu & Submenu");

	init ( );
	glutDisplayFunc (display);

	subMenu1 = glutCreateMenu (colorFcn);	// ສ້າງ​ Menu ​ຍ່ອຍ.
		glutAddMenuEntry ("Red", 1);
		glutAddMenuEntry ("Green", 2);
		glutAddMenuEntry ("Blue", 3);
		glutAddMenuEntry ("Black", 4);

	subMenu2 = glutCreateMenu (shapeFcn);	// ສ້າງ​ Menu ຍ່ອຍ.
		glutAddMenuEntry ("WireTorus", 1);
		glutAddMenuEntry ("WireSphere", 2);
		glutAddMenuEntry ("WireTeapot", 3);

	glutCreateMenu (mainMenu);				// ສ້າງ pop-up menu ຫຼັກ.
		glutAddMenuEntry ("White Blackground", 1);
		glutAddMenuEntry ("Yellow Blackground", 2);
		glutAddMenuEntry ("wht Blackground", 3);
		glutAddSubMenu ("Color", subMenu1);
		glutAddSubMenu ("Shape", subMenu2);

	/*  ໃຊ້ Menu ໂດຍ​ການ Click ຂວາແລ້ວ​ເລືອກ Menu.  */
	glutAttachMenu (GLUT_RIGHT_BUTTON);
	shape = color = 1;	  // ປ່ຽນ​ເປັນ​ລັກ​ສະ​ນະ ແລະ ສີ ທີ່​ໄດ້​ເລືອກ​ຈາກ Menu

	glutMainLoop ( );
}
