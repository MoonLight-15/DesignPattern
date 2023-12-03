# DesignPattern_Adapter
#include <iostream>
#include <string>
using namespace std;

// 새로운 비디오 플레이어 클래스
class VideoPlayer {
public:
    void playVideo(const std::string& videoFile) {
        cout << "Playing video: " << videoFile << endl;
    }
};

// 수정된 어댑터 클래스
class MediaAdapter : public MediaPlayer {
private:
    AudioPlayer audioPlayer;
    VideoPlayer videoPlayer; // 새로운 비디오 플레이어 추가
public:
    void play(const std::string& mediaFile) override {
        if (mediaFile.find(".mp3") != std::string::npos) {
            audioPlayer.playAudio(mediaFile);
        } else if (mediaFile.find(".mp4") != std::string::npos) {
            videoPlayer.playVideo(mediaFile);
        } else {
            cout << "Unsupported media format" << endl;
        }
    }
};

int main() {
    MediaPlayer* player = new MediaAdapter();
    player->play("song.mp3");
    player->play("movie.mp4");
    player->play("document.pdf"); // 지원하지 않는 형식

    delete player;
    return 0;
}
