# DesignPattern
#include <iostream>
using namespace std;

// 추상 클래스: 캐릭터
class Character {
public:
    virtual void startGame() = 0;
};

// 구체 클래스: 전사 캐릭터
class Warrior : public Character {
public:
    void startGame() override {
        cout << "전사: 게임 시작!" << endl;
    }
};

// 구체 클래스: 마법사 캐릭터
class Mage : public Character {
public:
    void startGame() override {
        cout << "마법사: 게임 시작!" << endl;
    }
};

// 팩토리 인터페이스
class CharacterFactory {
public:
    virtual Character* createCharacter() = 0;
};

// 구체 팩토리: 전사 캐릭터 팩토리
class WarriorFactory : public CharacterFactory {
public:
    Character* createCharacter() override {
        return new Warrior();
    }
};

// 구체 팩토리: 마법사 캐릭터 팩토리
class MageFactory : public CharacterFactory {
public:
    Character* createCharacter() override {
        return new Mage();
    }
};

// 클라이언트 코드
int main() {
    cout << "1. 전사 선택" << endl;
    cout << "2. 마법사 선택" << endl;

    int choice;
    cout << "캐릭터를 선택하세요 (1 또는 2): ";
    cin >> choice;

    CharacterFactory* characterFactory;

    if (choice == 1) {
        characterFactory = new WarriorFactory();
    }
    else if (choice == 2) {
        characterFactory = new MageFactory();
    }
    else {
        cout << "게임을 종료합니다." << endl;
        return 1;
    }

    Character* selectedCharacter = characterFactory->createCharacter();
    selectedCharacter->startGame();

    // 메모리 누수 방지를 위한 삭제
    delete selectedCharacter;
    delete characterFactory;

    return 0;
}
