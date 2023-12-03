# DesignPattern_Command
#include <iostream>
#include <vector>
using namespace std;

// Command 인터페이스
class Command {
public:
    virtual void execute() = 0;
};

// Receiver 클래스 - 불을 켜고 끄는 기능을 제공하는 클래스
class Light {
public:
    void turnOn() {
        cout << "불이 켜졌습니다." << endl;
    }

    void turnOff() {
        cout << "불이 꺼졌습니다." << endl;
    }
};

// ConcreteCommand 클래스 - 불을 켜는 명령
class TurnOnCommand : public Command {
private:
    Light* light;

public:
    TurnOnCommand(Light* l) : light(l) {}

    void execute() override {
        light->turnOn();
    }
};

// ConcreteCommand 클래스 - 불을 끄는 명령
class TurnOffCommand : public Command {
private:
    Light* light;

public:
    TurnOffCommand(Light* l) : light(l) {}

    void execute() override {
        light->turnOff();
    }
};

// Invoker 클래스 - 명령을 실행하는 클래스
class RemoteControl {
private:
    Command* command;

public:
    void setCommand(Command* cmd) {
        command = cmd;
    }

    void pressButton() {
        command->execute();
    }
};

int main() {
    // 불 객체 생성
    Light livingRoomLight;

    // 각각의 명령 객체 생성
    TurnOnCommand turnOnCommand(&livingRoomLight);
    TurnOffCommand turnOffCommand(&livingRoomLight);

    // Invoker 객체 생성
    RemoteControl remote;

    // 버튼을 눌러서 불을 켜기
    remote.setCommand(&turnOnCommand);
    remote.pressButton();

    // 버튼을 눌러서 불을 끄기
    remote.setCommand(&turnOffCommand);
    remote.pressButton();

    return 0;
}
