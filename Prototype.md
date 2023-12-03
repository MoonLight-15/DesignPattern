# DesignPattern_Prototype
#include <iostream>
using namespace std;

// 함수 프로토타입 선언
int add(int a, int b);
int subtract(int a, int b); // 새로운 함수 프로토타입

int main() {
    int resultAdd = add(20223418, 20223420); // add 함수 호출
    int resultSubtract = subtract(20223420, 20223418); // subtract 함수 호출

    // 결과 출력
    cout << "Addition Result: " << resultAdd << endl;
    cout << "Subtraction Result: " << resultSubtract << endl;

    return 0;
}

// 함수 정의
int add(int a, int b) {
    return a + b;
}

// 새로운 함수 정의
int subtract(int a, int b) {
    return a - b;
}
