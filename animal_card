#include <stdio.h>
#include <stdlib.h>
#include <time.h>
// 동물 카드 뒤집기
int arrayAnimal[4][5];// 5장씩 총 4줄 
int checkAnimal[4][5];// 뒤집혔는지 여부의 확인하는 배열
char* strAnimal[10];// 동물들의 이름이 들어갈 포인터 배열
void initAnimalArray();// 동물카드의 뒷면에 같은 값을 넣기 위한 함수
void initAnimalName();// 동뮬 카드를 이름을 초기화 하는 함수
void shuffleAnimal();// 카드 섞기 위한 함수
int getEmptyPosition();//카드 에서 빈 공간을 찾기 위한 함수
int conv_pos_x(int x);
int conv_pos_y(int y);
void printAnimals();
void printQuestion();


int main(void) {
	srand(time(NULL));
	initAnimalArray();// 뒷면에 -1 값 주기
	initAnimalName();// 앞면에 동물이름 초기화
	shuffleAnimal();
	int failCount = 0; //실패 횟수
	while (1) {
		int selected1 = 0;// 사용자가 선택한 수 1
		int selected2 = 0;// 사용자가 선탹한 수 2
		printAnimals(); // 동물 위치 출력
		printQuestion(); // 문제 출력
		printf("뒤집을 카드를 2개 고르세요: ");
		scanf_s("%d %d", &selected1, &selected2);
		if (selected1 == selected2) {// 같은 카드 선택 시 무효
			continue;
		}
		// 좌표에 해당하는 카드를 뒤집어 보고 같은지 다른지 확인.
		int firstSelected_x = conv_pos_x(selected1);
		int firstSelected_y = conv_pos_y(selected1);
		int secondSelected_x = conv_pos_x(selected2);
		int secondSelected_y = conv_pos_y(selected2);
		// 카드가 뒤집히지 않고 && 같은 동물인지
		// 카드가 다른 동물인지
		if ((checkAnimal[firstSelected_x][firstSelected_y] == 0 && checkAnimal[secondSelected_x][secondSelected_y] == 0) && 
			(arrayAnimal[firstSelected_x][firstSelected_y] == arrayAnimal[secondSelected_x][secondSelected_y])) {

			printf("\n\n 빙고! %s 발견 \n\n ", strAnimal[arrayAnimal[firstSelected_x][firstSelected_y]]);
			checkAnimal[firstSelected_x][firstSelected_y] = 1;
			checkAnimal[secondSelected_x][secondSelected_y] = 1;


		}
		else {
			printf("\n\n 땡! 서로 다른 동물 카드이거나 이미 뒤집힌 카드 입니다.\n ");
			printf("%d : %s\n", selected1, strAnimal[arrayAnimal[firstSelected_x][firstSelected_y]]);
			printf("%d : %s\n", selected2, strAnimal[arrayAnimal[secondSelected_x][secondSelected_y]]);
			printf("\n\n");
			failCount++;
		}
		//모든 동물을 다 찾은 경우
		// 게임을 끝내야함
		// 
		if (foundAllAnimals() == 1) {
			printf("\n\n 축하합니다. ! 모든 동물을 다 찾았습니다.\n");
			printf("\n\n 지금까지 총 %d 번 실수 했습니다.\n", failCount);
			break;
		}

	}
	return 0;
}

void initAnimalArray() {
	for (int i = 0; i < 4; i++) {
		for (int j = 0; j < 5; j++) {
			arrayAnimal[i][j] = -1; // 카드의 모든 뒷면에 -1 값 넣기
		}
	}
}
void initAnimalName() {
	strAnimal[0] = "원숭이";
	strAnimal[1] = "하마";
	strAnimal[2] = "강아지";
	strAnimal[3] = "고양이";
	strAnimal[4] = "돼지";
	strAnimal[5] = "코끼리";
	strAnimal[6] = "기린";
	strAnimal[7] = "낙타";
	strAnimal[8] = "타조";
	strAnimal[9] = "호랑이";
}
void shuffleAnimal() {
	// 총10번 실행 2번씩 결과 넣기 총 20개
	//arrayAnimal 배열의 랜덤한 위치에 값을 넣기 위한 함수
	for (int i = 0; i < 10;i++) {
		for (int j = 0; j < 2;j++) {
			int pos = getEmptyPosition();//카드 에서 빈 공간을 찾기 위한 함수
			int x = conv_pos_x(pos);// 그 공간을 x좌표로 반환하는 함수 호출
			int y = conv_pos_y(pos);// 그 공간을 y좌표로 반환하는 함수 호출
			arrayAnimal[x][y] = i;// 2차원 공간에 같은 카드에 같은 값을 넣어준다.
		}
	}
}
int getEmptyPosition() {
	//shuffleAnimal()의 x,y 값에 들어갈 랜덤 좌표를 생성하는 함수
	while (1) {
		int randPos = rand() % 20;// 0~ 19 사이 숫자 생성
		int x = conv_pos_x(randPos);
		int y = conv_pos_y(randPos);
		if (arrayAnimal[x][y] == -1) {// 2차원 공간이 비어있다면
			return randPos;
		}
	}
	return 0;
}
int conv_pos_x(int x) {
	return x / 5;
}
int conv_pos_y(int y) {
	return y % 5;
}

void printAnimals() { // 동물 위치 출력 함수
	printf("\n ===========동물 위치를 보여줍니다. ============\n\n");
	for (int i = 0; i < 4;i++) {
		for (int j = 0; j < 5; j++) {
			printf("%8s", strAnimal[arrayAnimal[i][j]]);
		}
		printf("\n");
	}
	printf("\n=================================================\n");
}

void printQuestion() {
	printf("\n(문제)\n\n");
	int seq = 0;
	for (int i = 0; i < 4; i++) {
		for (int j = 0; j < 5; j++) {
			// 카드를 뒤집어서 정답이면 '동물이름' 출력
			// 
			if (checkAnimal[i][j] != 0) {// 카드가 앞면이면
				printf("%8s", strAnimal[arrayAnimal[i][j]]);
			}
			// 아직 뒤집지 못했다면 (정답을 맞추지 못했다면) 뒷면 -> 숫자를 나타내는 숫자
			else {
				printf("%8d", seq);
			}
			seq++;
		}
		printf("\n");
	}
}
int foundAllAnimals() {
	for (int i = 0; i < 4; i++) {
		for (int j = 0; j < 5; j++) 
		{
			// 만약에 다 뒤집혔다면
			if (checkAnimal[i][j] == 0) {
				return 0;
			}
		}
	}
	return 1; // 모든 동물을 다 찾음;
}
