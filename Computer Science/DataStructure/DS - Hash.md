# 해시 Hash
- 데이터를 최대한 빠른 속도로 관리하도록 도와주는 자료 구조 
- 메모리 공간이 많이 소모되지만 매우 빠른 속도로 데이터를 처리할 수 있다
- 빠르게 데이터에 접근할 수 있따는 점에서 데이터베이스 등의 소프트웨어에서 활용됨 
- 특정한 값(Value)를 찾고자 할 때는 그 값의 키(Key)로 접근할 수 있다
- 일반적으로 해시 함수는 모듈로(modulo) 연산 등의 수학적 연산으로 이루어져 있으므로 O(1)만에 값에 접근할 수 있다
- 해시테이블에서 key가 중복되는 경우 충돌(Collision)이 발생했다고 표현함
- 나눗셈 법이 가장 많이 활용됨 ->  입력 값을 테이블의 크기로 나눈 나머지를 키로 사용하는 방법
- 테이블의 크기는 소수(Prime Number)로 설정하는 것이 효율이 좋다
- 충돌을 처리하는 방법
	- 충돌을 발생시키는 항목을 해시 테이블의 다른 위치에 저장
		- 선형 조사법 : 바로 다음 위치에
		- 이차 조사법 : 키 값을 선택할 때 '완전 제곱수'를 더해 나가는 방식
	- 해시 테이블의 하나의 버킷에 여러 개의 항목을 저장   
		- 체이닝 : 연결 리스트를 활용해 특정한 키를 가지는 항목들을 연결하여 저장, 삽입과 삭제가 쉽다, 테이블 크기 재설정 문제는 '동적 할당'으로 손쉽게 해결(추가적인 메모리 소모)

### 선형조사법
- 충돌이 발생하기 시작하면, 유사한 값을 가지는 데이터끼리 서로 밀집되는 집중 결합문제가 있음
- '해시 테이블의 크기'가 비약적으로 크면(메모리를 많이 소모) 충돌이 적게 발생하므로 매우 빠른 데이터 접근 속도를 가질 수 있지만, 일반적인 경우 해시 테이블의 크기는 한정적이므로 충돌이 최대한 적게 발생하도록 해야 함

``` c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define TABLE_SIZE	10007
#define INPUT_SIZE	5000

typedef struct {
	int id;
	char name[20];
} Student;

// 해시 테이블 초기화
void init(Student** hashTable) {
	for (int i = 0; i < TABLE_SIZE; i++) {
		hashTable[i] = NULL;
	}
}

// 해시 테이블의 메모리를 반환
void destructor(Student** hashTable) {
	for (int i = 0; i < TABLE_SIZE; i++) {
		if (hashTable[i] != NULL) {
			free(hashTable[i]);
		}
	}

}

//해시 테이블 내 빈 공간을 선형 탐색으로 찾음
int findEmpty(Student** hashTable, int id) {
	int i = id % TABLE_SIZE;
	while (1) {
		if (hashTable[i % TABLE_SIZE] == NULL) {
			return i % TABLE_SIZE;
		}
		i++;
	}
}

// 특정한 ID 값에 매칭되는 데이터를 해시 테이블 내에서 찾는다
int search(Student** hashTable, int id) {
	int i = id % TABLE_SIZE;
	while (1) {
		if (hashTable[i % TABLE_SIZE] == NULL) return -1;
		else if (hashTable[i % TABLE_SIZE]->id == id) return i;
		i++;
	}
}

// 특정한 키 인덱스에 데이터를 삽입
void add(Student** hashTable, Student* input, int key) {
	hashTable[key] = input;
}

// 해시 테이블에서 특정한 키의 데이터를 반환
Student* getValue(Student** hashTable, int key) {
	return hashTable[key];
}

// 출력
void show(Student** hashTable) {
	for (int i = 0; i < TABLE_SIZE; i++) {
		if (hashTable[i] != NULL) {
			printf("키: [%d] 이름: [%s]\n", i, hashTable[i]->name);
		}
	}
}

int main(void) {
	Student** hashTable;
	hashTable = (Student**)malloc(sizeof(Student) * TABLE_SIZE);
	init(hashTable);

	for (int i = 0; i < INPUT_SIZE; i++) {
		Student* student = (Student*)malloc(sizeof(Student));
		student->id = rand() % 10000000;
		sprintf(student->name, "사람%d", student->id);
		if (search(hashTable, student->id) == -1) {
			int index = findEmpty(hashTable, student->id);
			add(hashTable, student, index);
		}
	}

	show(hashTable);
	destructor(hashTable);
	
	system("pause");
	return 0;
}
}
```
### 체이닝
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define TABLE_SIZE	10007
#define INPUT_SIZE	5000

typedef struct {
	int id;
	char name[20];
} Student;


typedef struct {
	Student* data;
	struct Bucket* next;
} Bucket;

// 초기화
void init(Bucket** hashTable) {
	for (int i = 0; i < TABLE_SIZE; i++) {
		hashTable[i] = NULL;
	}
}

// 메모리 반환
void destructor(Bucket** hashTable) {
	for (int i = 0; i < TABLE_SIZE; i++) {
		if (hashTable[i] != NULL) {
			free(hashTable[i]);
		}
	}
}

// 검색
int isExist(Bucket** hashTable, int id) {
	int i = id % TABLE_SIZE;
	if (hashTable[i] == NULL) return 0;
	else {
		Bucket* cur = hashTable[i];
		while (cur != NULL) {
			if (cur->data->id == id) return 1;
			cur = cur->next;
		}
	}
	return 0;
}
// 삽입
void add(Bucket** hashTable, Student* input) {
	int i = input->id % TABLE_SIZE;
	if (hashTable[i] == NULL) {
		hashTable[i] = (Bucket*)malloc(sizeof(Bucket));
		hashTable[i]->data = input;
		hashTable[i]->next = NULL;
	}
	else {
		Bucket* cur = (Bucket*)malloc(sizeof(Bucket));
		cur->data = input;
		cur->next = hashTable[i];
		hashTable[i] = cur;
	}
		
}

// 출력
void show(Bucket** hashTable) {
	for (int i = 0; i < TABLE_SIZE; i++) {
		if (hashTable[i] != NULL) {
			Bucket* cur = hashTable[i];
			while (cur != NULL) {
				printf("키: [%d] 이름:[%s]\n", i, cur->data->name);
				cur = cur->next;
			}
		}
	}
}

int main(void) {
	Bucket** hashTable;
	hashTable = (Bucket**)malloc(sizeof(Bucket) * TABLE_SIZE);
	init(hashTable);
	for (int i = 0; i < INPUT_SIZE; i++) {
		Student* student = (Student*)malloc(sizeof(Student));
		student->id = rand() % 1000000;
		sprintf(student->name, "사람%d", student->id);
		if (!isExist(hashTable, student->id)) { // 중복되는 ID는 존재하지 않도록 함.
			add(hashTable, student);
		}
	}
	show(hashTable);
	destructor(hashTable);
	system("pause");
	return 0;
}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]