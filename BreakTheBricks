#include <graphics.h>
#include <conio.h>
#include <stdlib.h>
#include <time.h>

#define UP 72
#define DOWN 80
#define LEFT 75
#define RIGHT 77
#define WIDTH 640
#define HEIGHT 550
#define PADDLE_HEIGHT 20
#define BALL_SIZE 8

// Constants
const int BRICK_WIDTH = 30;
const int BRICK_HEIGHT = 15;
const int GAP = 5;
const int NORMAL_BRICK = 0;
const int SPECIAL_BRICK = 1; // red
const int SPECIAL_BRICK2 = 2; // green
const int SPECIAL_BRICK3 = 3; //blue

// Global variables
int totalBricks = 56;
int numBricks = 72;
int bricks[5][10]; // for "easy"
int bricks2[56][3]; // for "medium" 
int bricks3[72][3]; // for "hard" 
int paddle_x = WIDTH / 2;
int paddle_y = HEIGHT - 30;
int ball_x = WIDTH / 2;
int ball_y = paddle_y - 120;
int dx = 5;
int dy = 5;
int score = 0;
int lives = 3; // Initial number of lives
int paused = 0;
int PADDLE_WIDTH = 100;


//COMMON
void drawPaddle() {
    setfillstyle(SOLID_FILL, LIGHTBLUE);
    bar(paddle_x, paddle_y, paddle_x + PADDLE_WIDTH, paddle_y + PADDLE_HEIGHT);
}

void drawBall() {
    setfillstyle(SOLID_FILL, RED);
    fillellipse(ball_x, ball_y, BALL_SIZE, BALL_SIZE);
}
void input() {
    if (kbhit()) {
        switch (getch()) {
        case 32:
            paused = !paused;
            break;
        }
    }

    if (!paused) {
        if (kbhit()) {
            switch (getch()) {
            case LEFT:
                paddle_x -= 60;
                break;
            case RIGHT:
                paddle_x += 60;
                break;
            }
        }
    }

    if (paddle_x <= 0) {
        paddle_x = 0;
    }
    if (paddle_x >= 540) {
        paddle_x = 540;
    }
}

//EASY_LEVEL
void initialize(int rows, int cols) {
    int i, j;

    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            bricks[i][j] = 1;
        }
    }
}

void move() {
    if (!paused) {
        int i, j;

        ball_x += dx;
        ball_y += dy;

        if (ball_x >= paddle_x && ball_x <= paddle_x + PADDLE_WIDTH && ball_y >= paddle_y - BALL_SIZE && ball_y <= paddle_y) {
            dy = -dy;
        }

        for (i = 0; i < 5; i++) {
            for (j = 0; j < 10; j++) {
                if (bricks[i][j] == 1) {
                    if (ball_x >= j * 60 + 10 && ball_x <= j * 60 + 60 && ball_y >= i * 20 + 10 && ball_y <= i * 20 + 30) {
                        bricks[i][j] = 0;
                        dy = -dy;
                        score++;
                    }
                }
            }
        }
    }

    if (ball_x <= 0 || ball_x >= 600) {
        dx = -dx;
    }

    if (ball_y <= 0) {
        dy = -dy;
    }
    int page = 0;
    if (ball_y >= getmaxy()) {
        lives--;
        if (lives <= 0) {
        	setactivepage(page);
			clearviewport();
            outtextxy(200, HEIGHT/2 - 30, "Game Over");
            outtextxy(200, HEIGHT/2, "Press any key.");
            getch();
            closegraph();
            exit(0);
        } else {
            getch();
			ball_x = paddle_x + 20;
            ball_y = paddle_y - 30;
            dx = -dx;
            dy = -dy;
        }
    }
    if (score == 50) {
        setactivepage(page);
		clearviewport();
		outtextxy(150, HEIGHT/2, "Congratulations! You won the game.");
        getch();
        closegraph();
        exit(0);
    }

   
}

void draw() {
    int i, j;

    cleardevice();
    drawPaddle();
    drawBall();

    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 10; j++) {
            if (bricks[i][j] == 1) {
                 if (i == 0) {
                    setfillstyle(SOLID_FILL, COLOR(125, 125, 55));
                } else if (i == 1) {
                    setfillstyle(SOLID_FILL, COLOR(55, 55, 125));
                } else if (i == 2) {
                    setfillstyle(SOLID_FILL, DARKGRAY);
                } else if (i == 3) {
                    setfillstyle(SOLID_FILL, CYAN);
                } else if (i == 4) {
                    setfillstyle(SOLID_FILL, MAGENTA);
                }
                bar(j * 60 + 18, i * 20 + 18, j * 60 + 63, i * 20 + 33);
            }
        }
    }

    char text[50];
    settextstyle(BOLD_FONT, HORIZ_DIR, 1);
    sprintf(text, "%d", score);
    outtextxy(5, 0, "Score:");
    outtextxy(75, 0, text);

    sprintf(text, "Lives: %d", lives);
    outtextxy(500, 0, text);

    if (paused) {
        outtextxy(325, 270, "Paused");
    }
}
//MEDIUM LEVEL
void initialize2() {
    srand(time(NULL));  

    int x = 75, y = 25, row = 7, col = 7, bricksCount = 0;
    int specialBrickPos = rand() % 28;   
    int specialBrick2Pos = rand() % (56 - 29 + 1) + 29;  

    // First set of bricks
    for (int i = 1; i <= row; i++) {
        for (int j = col; j >= 1; j--) {
            bricks2[bricksCount][0] = x;
            bricks2[bricksCount][1] = y;
            if (bricksCount == specialBrickPos) {
                bricks2[bricksCount][2] = SPECIAL_BRICK;
            } else {
                bricks2[bricksCount][2] = NORMAL_BRICK;
            }

            bricksCount++;
            x += BRICK_WIDTH + GAP;
        }
        col--;
        y += BRICK_HEIGHT + GAP;
        x = 75 + i * BRICK_WIDTH / 2;
    }

    x = 320, y = 25, row = 7, col = 7;

    // Second set of bricks
    for (int i = 1; i <= row; i++) {
        for (int j = col; j >= 1; j--) {
            bricks2[bricksCount][0] = x;
            bricks2[bricksCount][1] = y;
            if (bricksCount == specialBrick2Pos) {
                bricks2[bricksCount][2] = SPECIAL_BRICK2;
            } else {
                bricks2[bricksCount][2] = NORMAL_BRICK;
            }

            bricksCount++;
            x += BRICK_WIDTH + GAP;
        }
        col--;
        y += BRICK_HEIGHT + GAP;
        x = 320 + i * BRICK_WIDTH / 2;
    }
}


void move2() {
    if (!paused) {
        
        ball_x += dx;
        ball_y += dy;

        if (ball_x < 20 || ball_x > getmaxx() - BALL_SIZE) {
            dx = -dx;
        }
        if (ball_y < 25) {
            dy = -dy;
        }

        if (ball_x >= paddle_x && ball_x <= paddle_x + PADDLE_WIDTH && ball_y >= paddle_y - BALL_SIZE && ball_y <= paddle_y) {
            dy = -dy;
        }

        for (int i = 0; i < totalBricks+1; i++) {
            if (bricks2[i][0] <= ball_x  && ball_x  <= bricks2[i][0] + BRICK_WIDTH &&
                bricks2[i][1] <= ball_y  && ball_y  <= bricks2[i][1] + BRICK_HEIGHT) {
                dy = -dy;
                score++;

                if (bricks2[i][2] == SPECIAL_BRICK) {
                    PADDLE_WIDTH += 30; // Increase paddle length by 30 units (red)
                } else if (bricks2[i][2] == SPECIAL_BRICK2) {
                    lives += 1; // Gain 1 extra life (green)
                } else if (bricks2[i][2] == SPECIAL_BRICK3) {
                    dx += (dx > 0) ? 2 : -2; // Speed Up (blue)
                    dy += (dy > 0) ? 2 : -2;
                }

                bricks2[i][0] = -100; // Move the brick off-screen
                bricks2[i][1] = -100;
                break;
            }
        }
    }
     int page = 0;
    if (ball_y > getmaxy()) {
        lives--;
        if (lives <= 0) {
            setactivepage(page);
            clearviewport();
			outtextxy(200, HEIGHT / 2, "Game Over");
            outtextxy(200, HEIGHT / 2 + 30, "Press any key to exit");
            getch();
            closegraph();
            exit(0);
        } else {
            ball_x = paddle_x + 20;
            ball_y = paddle_y - 30;
            dx = -dx;
            dy = -dy;
        }
    }
     
    if (score == totalBricks) {
        setactivepage(page);
        clearviewport();
		outtextxy(150, HEIGHT / 2, "Congratulations! You won the game.");
        getch();
        closegraph();
        exit(0);
    }
}


void drawBrick2(int x, int y, int type = NORMAL_BRICK) {
    int color;
    if (type == SPECIAL_BRICK) {
        color = COLOR(255, 0, 0); 
    } else if (type == SPECIAL_BRICK2) {
        color = COLOR(0, 255, 0);
    }
    else if (type == SPECIAL_BRICK3) {
        color = COLOR(0, 0, 255);
    }
    else
    {
        color = COLOR(255, 255, 0);
    }

    setfillstyle(SOLID_FILL, color);
    bar(x, y, x + BRICK_WIDTH, y + BRICK_HEIGHT);
}

void draw2() {
    int i, j;

    cleardevice();
    drawPaddle();
    drawBall();

    for (int i = 0; i <= totalBricks; i++) {
                drawBrick2(bricks2[i][0], bricks2[i][1], bricks2[i][2]);
            }

    char text[50];
    settextstyle(BOLD_FONT, HORIZ_DIR, 1);
    sprintf(text, "%d", score);
    outtextxy(5, 0, "Score:");
    outtextxy(75, 0, text);

    sprintf(text, "Lives: %d", lives);
    outtextxy(500, 0, text);

    if (paused) {
        outtextxy(325, HEIGHT/2, "Paused");
    }
}
//HARD_LEVEL
void initialize3() {
    srand(time(NULL));
	int x = 50, y = 25, row = 0, col = 0;
	int specialBrickPos = rand() % 11;   
    int specialBrick2Pos = rand() % (23 - 12 + 1) + 12;
    int specialBrick3Pos = rand() % (35 - 24 + 1) + 24;  
    for (int i = 0; i < 36; i++) {
        bricks3[i][0] = x;
        bricks3[i][1] = y;
        
        if (i == specialBrickPos) {
            bricks3[i][2] = SPECIAL_BRICK; 
        } else if ( i == specialBrick2Pos) {
            bricks3[i][2] = SPECIAL_BRICK2;
        } else if ( i == specialBrick3Pos){
            bricks3[i][2] = SPECIAL_BRICK3;
        }
        else
        {
            bricks3[i][2] = NORMAL_BRICK;
        }

        x += BRICK_WIDTH + GAP;
        col++;
        if (col > row) {
            x = 50;
            y += BRICK_HEIGHT + GAP;
            row++;
            col = 0;
        }
    }

    x = 60;
    y = 25;
    row = 0;
    col = 0;
     specialBrickPos = rand() % (47 - 36 + 1) + 36;   
     specialBrick2Pos = rand() % (59 - 48 + 1) + 48;
     specialBrick3Pos = rand() % (71 - 60 + 1) + 60;  

    for (int i = 36; i < numBricks; i++) {
        bricks3[i][0] = getmaxx() - x;
        bricks3[i][1] = y;

        if (i == specialBrickPos) {
            bricks3[i][2] = SPECIAL_BRICK; 
        } else if (  i == specialBrick2Pos) {
            bricks3[i][2] = SPECIAL_BRICK2;
        } else if ( i == specialBrick3Pos) {
            bricks3[i][2] = SPECIAL_BRICK3;
        }
        else
        {
            bricks3[i][2] = NORMAL_BRICK;
        }

        x += BRICK_WIDTH + GAP;
        col++;
        if (col > row) {
            x = 60;
            y += BRICK_HEIGHT + GAP;
            row++;
            col = 0;
        }
    }
}


void move3() {
    if (!paused) {
        ball_x += dx;
        ball_y += dy;

        if (ball_x < 0 || ball_x > getmaxx() - BALL_SIZE) {
            dx = -dx;
        }
        if (ball_y < 0) {
            dy = -dy;
        }

        if (ball_x >= paddle_x && ball_x <= paddle_x + PADDLE_WIDTH && ball_y >= paddle_y - BALL_SIZE && ball_y <= paddle_y ) {
            dy = -dy;
        }

        for (int i = 0; i < numBricks; i++) {
            if (bricks3[i][0] <= (ball_x ) && (ball_x ) <= bricks3[i][0] + BRICK_WIDTH &&
                bricks3[i][1] <= (ball_y ) && (ball_y ) <= bricks3[i][1] + BRICK_HEIGHT) {
                dy = -dy;
                score++;

                if (bricks3[i][2] == SPECIAL_BRICK) {
                    PADDLE_WIDTH += 15; // Increase paddle length by 30 units (red)
                } else if (bricks3[i][2] == SPECIAL_BRICK2) {
                    lives += 1; // Gain 1 extra life (green)
                } else if (bricks3[i][2] == SPECIAL_BRICK3) {
                    dx += (dx > 0) ? 1 : -1; // Speed Up (blue)
                    dy += (dy > 0) ? 1 : -1;
                }

                bricks3[i][0] = -100; // Move the brick off-screen
                bricks3[i][1] = -100;
                break;
            }
        }
    }
     int page = 0;
    if (ball_y > getmaxy()) {
        lives--;
        if (lives <= 0) {
            setactivepage(page);
        	clearviewport();
			outtextxy(200, HEIGHT / 2, "Game Over");
            outtextxy(200, HEIGHT / 2 + 30, "Press any key to exit");
            getch();
            closegraph();
            exit(0);
        } else {
            ball_x = paddle_x + 20;
            ball_y = paddle_y - 30;
            dx = -dx;
            dy = -dy;
        }
    }

    if (score == numBricks) {
        setactivepage(page);
		clearviewport();
		outtextxy(150, HEIGHT / 2, "Congratulations! You won the game.");
        getch();
        closegraph();
        exit(0);
    }
}


void drawBrick3(int x, int y, int type = NORMAL_BRICK) {
    int color;
    if (type == SPECIAL_BRICK) {
        color = COLOR(255, 0, 0); 
    } else if (type == SPECIAL_BRICK2) {
        color = COLOR(0, 255, 0);
    }
    else if (type == SPECIAL_BRICK3) {
        color = COLOR(0, 0, 255);
    }
    else
    {
        color = COLOR(0, 255, 255);
    }

    setfillstyle(SOLID_FILL, color);
    bar(x, y, x + BRICK_WIDTH, y + BRICK_HEIGHT);
}

void draw3() {
    int i, j;

    cleardevice();
    drawPaddle();
    drawBall();

    for (int i = 0; i < numBricks; i++) {
                drawBrick3(bricks3[i][0], bricks3[i][1], bricks3[i][2]);
            }

    char text[50];
    settextstyle(BOLD_FONT, HORIZ_DIR, 1);
    sprintf(text, "%d", score);
    outtextxy(5, 0, "Score:");
    outtextxy(75, 0, text);

    sprintf(text, "Lives: %d", lives);
    outtextxy(500, 0, text);

    if (paused) {
        outtextxy(325, HEIGHT/2, "Paused");
    }
}
//Function for easy level
void easyLevel() {
	lives--;
	initialize(5, 10);
        int page = 0;
        while (1) {
            setactivepage(page);
            setvisualpage(1 - page);
            draw();
            input();
            move();
            page = 1 - page;
            delay(6);
}
}
//Function for medium level
void mediumLevel() {
	initialize2();
        int page = 0;
        while (1) {
            setactivepage(page);
            setvisualpage(1 - page);
            draw2();
			input();
			move2();
            
			page = 1 - page;
            delay(6);
}
}
//Function for hard level
void hardLevel() {
	initialize3();
        int page = 0;
        while (1) {
            setactivepage(page);
            setvisualpage(1 - page);
            
			draw3();
			input();
			move3();
            
			page = 1 - page;
            delay(6);
}
}
void playGame(){
	setbkcolor(BLUE);
	setcolor(YELLOW);
	clearviewport();
	settextstyle(BOLD_FONT, HORIZ_DIR, 2);
	outtextxy(100, HEIGHT/2-50, "Please enter '1' to start the game");
    outtextxy(100, HEIGHT/2 -20, "Please enter '2' for instructuions");
	outtextxy(100, HEIGHT/2 +10, "Please enter '0' to exit");
    int select = getch() - '0';
    clearviewport();

    if (select == 1) {
        setbkcolor(BLUE);
        clearviewport();
        settextstyle(BOLD_FONT, HORIZ_DIR, 2);
        outtextxy(200, 200, "Choose a level:");
        outtextxy(200, 230, "1. Easy");
        outtextxy(200, 260, "2. Medium");
        outtextxy(200, 290, "3. Hard");

        int choice = getch() - '0';
        setbkcolor(BLACK);
    if (choice == 1) {
        easyLevel();
        }
     else if (choice == 2) {
        mediumLevel();
        }
    
    else if (choice == 3) {
        hardLevel();
        }
     else {
        setbkcolor(BLUE);
		clearviewport();
		outtextxy(200, 200, "Invalid choice.");
        getch();
        playGame();
    }
}
    
    else if(select == 2){
    	setbkcolor(BLUE);
        clearviewport();
        settextstyle(BOLD_FONT, HORIZ_DIR, 6);
		int y=70;
		outtextxy(140, y, "INSTRUCTIONS");
		settextstyle(BOLD_FONT, HORIZ_DIR, 1);
        y = y+ 50;
		outtextxy(20, y+20, "1.Control the paddle using the Left & Right arrow keys.");
		outtextxy(20, y+50, "2.Break the bricks by hitting them with the ball."); 
		outtextxy(20, y+80, "3.Each hit removes the brick and increases your score.");
        outtextxy(20, y+110, "4.Some levels feature Special Bricks.");
        outtextxy(20, y+140, "	   ~Red Brick: Increases the width of your paddle.");
        outtextxy(20, y+170, "	   ~Green Brick: Grants an extra life.");
        outtextxy(20, y+200, "	   ~Blue Brick: Increases the speed of the ball.");
        outtextxy(20, y+250, "	**CLICK ANYWHERE TO RETURN TO THE MAIN MENU**");
		
		getch();
        playGame();
        }
    else if(select == 0)
    {
    	 int k;
		 outtextxy(100, HEIGHT/2-60, "Do you really want to exit?");
    	 outtextxy(100, HEIGHT/2-30, "1.YES          2.NO");
		 k = getch() - '0';
		 if(k==1)
		 {
		 cleardevice();
		 setbkcolor(BLUE);
		 outtextxy(300, HEIGHT/2-30, "EXITING...");
    	 delay(2000);
		 closegraph();
    	 exit(0);
         }
         else if(k==2)
         {
         	playGame();
		 }
	}
	else
	{
		outtextxy(220, HEIGHT/2-30, "INVALID CHOICE....");
		getch();
		playGame();
	}
	
	
}
int main() {
    initwindow(WIDTH, HEIGHT, "BREAK_THE_BRICKS");
    setbkcolor(BLUE);
    
	clearviewport();
    settextstyle(BOLD_FONT, HORIZ_DIR, 6);
    setcolor(YELLOW);
	outtextxy(190, 170, "WELCOME"); 
	outtextxy(270, 220, "TO");
	outtextxy(70, 270, "BREAK THE BRICKS");
	setfillstyle(SOLID_FILL, YELLOW);
	rectangle(50,100,590,400);
	rectangle(25,75,615,425);
	getch();
	playGame();
    
	closegraph();
    getch();
    return 0;
}
