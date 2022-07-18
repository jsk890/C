#include <stdio.h>
#include <windows.h> // VK_KEY 사용
#include <time.h>
#include <conio.h> // _kbhit()사용
#include <stdlib.h> // mode con 사용
#include <locale.h> // _wsetlocale
#pragma comment(lib,"winmm.lib") // timeGetTime() 사용
 
#define SOUND_TITLE_NAME "Bassa Island Game" // 타이틀 bgm 파일 이름 지정
#define SOUND_MENU_NAME "MenuSelect"
#define SOUND_STORE_NAME "Sunset Strip"
#define SOUND_SINGLE_NAME "Single Effect"
#define SOUND_CONTINUE_NAME "Water Bubbling Effect"
 
#define SOUND_WHOLE_NAME "Explosions Effect"
#define SOUND_GAMEEXIT_NAME "Bomba Pa Siempre Sting"
#define SOUND_GAMEOVER_NAME "The Story Unfolds Sting"
#define SOUND_STORYSTART_NAME "Ersatz Bossa Sting"
#define SOUND_STORYEND_NAME "Cartoon Bank Heist Sting"
#define SOUND_PLARYAPPEAR_NAME "Cinematic Sting"
#define SOUND_PLARYSPEAK_NAME "Prelude_No_20"
#define SOUND_CHAPTER2_NAME "African Drums Sting"
#define SOUND_OWNERAPPEAR_NAME "Laconic Granny"
 
#define IMG_H 74 // 이미지 세로줄
#define IMG_W 55 // 이미지 가로줄
#define TOTAL_FRAME 14 // 전체 프레임 개수
#define FISH_MAX 6      // 물고기 최대수
#define MAP_HEIGHT 20   // 맵크기
#define MAP_WIDTH 30
#define TAP_HEIGHT 10   // 인터페이스 크기
#define TAP_WIDTH 30
#define POPUP_HEIGHT 25   // 팝업창 크기
#define POPUP_WIDTH 16
#define POPUPSTART_POSX 38 // 팝업창 출력시작 좌표
#define POPUPSTART_POSY 18
#define STORY_HEIGHT 24 // 스토리창 크기
#define STORY_WIDTH    16
#define STORYSTART_POSX 70 // 스토리창 출력 시작 좌표
#define STORYSTART_POSY 4 
#define PLARY_POSX 37   // 플라리 초기 위치
#define PLARY_POSY 14
#define TAB_COLOR 14   // 탭 색깔
#define RESET_COLOR 15   // 원래 색깔
#define enter while (1){scanf_s("%c", &cEnter,1); if (cEnter == '\n') break;} //엔터 수동입력
 
/*
파랑 1/9, 초록 2/10, 하늘 3/11, 빨강 4/12
분홍 5/13, 노랑 6/14, 흰색 7/15, 회색 8
*/
 
// 멜로디 음계(Beep 함수)
#define _C 1046.502
#define _D 1108.731
#define _E 1318.510
#define _F 1396.913
#define _G 1567.982
#define _A 1760.000
#define _B 1975.533
 
int g_arrMap[MAP_HEIGHT][MAP_WIDTH] = {// 플레이 화면 모양
    { 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 5,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,6 }
};
 
int g_arrTap[TAP_HEIGHT][TAP_WIDTH] = {// 탭 화면 모양
    { 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 5,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,6 }
};
 
int g_arrPopup[POPUP_HEIGHT][POPUP_WIDTH] = {// 가이드 모양
    { 3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,4 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 5,2,2,2,2,2,2,2,2,2,2,2,2,2,2,6 },
};
 
int g_arrStory[STORY_HEIGHT][STORY_WIDTH] = {
    { 3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,4 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1 },
    { 5,2,2,2,2,2,2,2,2,2,2,2,2,2,2,6 }, };
 
// 탭 키관리, 플라리 방향, 플라리 레벨, 가진 세포수, 단백질, 사용되는 세포, 가이드키 동작조절
int iTapSelect = 0, iDir = 0, iLevel = 1, iCell = 2, iProtein = 0, iCellUseUp = 0, iF1 = 0;
// 물고기 갱신 관리
int i1FishDie = 0, i2FishDie = 0;
// 스킬 세포 소모 관리
int iSingleSkill = 0, iCountinuousSkill = 0, iWholeSkill = 0, iArtificiality = 0;
// 경험치바 채우기, 물고기 근접처리, 게임오버 처리
int iExpFulling = 0, iFishNear1 = 0, iFishNear2 = 0, iGameover = 0;
// 현재 경험치 비율, 이전경험치 상한선, 현재경험치 상한선, 현재레벨 이후 경험치 누적정보, 레벨업시 현재 상한선 초과 경험치분 저장, 모은 경험치
float fBlock = 0, fPrevExpLimits = 0, fCurExpLimits = 0, fElapsedExp = 0, fExtraElapesExp = 0, fLeftExp = 0, fTotalExp = 0;
typedef enum _TAP { Info, CellLab, Rank, TheNum_MENU }TAP; // 탭 메뉴관리
short int curt, prev, push, pull; //단일공격 변수
 
typedef enum _DIR { L, R, DIR_LEN }DIR; // 방향 관리
typedef struct _SVector
{
    float fX, fY; // 벡터로 방향 설정
}SVector;
 
const SVector g_arrDir[DIR_LEN] =
{
    { -1.0f,0.0f }, // 왼쪽
    { 1.0f,0.0f }   // 오른쪽
};
 
typedef struct _SFish
{
    float fPosX;   // 물고기 x좌표
    float fPosY;   // 물고기 y좌표
    float fAttack;   // 물고기 공격력
    double dSpeed;   // 물고기 이동속도
    float fHunger;   // 물고기 배고픔 정도
    float fExp;      // 물고기에게서 얻을 경험치
    float fProtein;   // 물고기에게서 얻는 (단백질)돈
    DIR dir;      // 물고기 방향
}SFish;
SFish g_arrFish[FISH_MAX];   // 물고기 배열 준비
 
int PrintTitle(int _s);                // 타이틀 화면 구성하기
int PrintSoundOptions(int _s);            // 소리 on off 관리
int PrintPlayScreenInit(int _s);        //초기 플레이 화면 구성하기
int PrintPlayScreen(int _s);               // 플레이 속도 조절
int PrintStoryQuest(int _s);            //스토리 진행 함수
void PrintStory();                        //  스토리 창을 그리는 함수
int Chapter1(int _s);
int Chapter2(int _s);
void PrintMap(int _height, int _width);   // 어항(플레이 맵)을 그리는 함수
void PrintTap(int _height, int _width);   // 탭 인터페이스를 그리는 함수
int PrintTapInterface(int _s);            // 탭 모양 및 색깔을 그리는 함수
void InputKeyManager(int _x, int _y);   // 플레이시에 플라리 방향 처리
void PrintInfoTap();               // 인포 탭
int PrintCellLabTap(int _s);               // 상점 탭
void PrintSkillTap();               // 스킬 탭
void FishInit1();                  // 물고기 초기 정보
void FishInit2();
void FishUpdate1(DWORD _curTime);            // 물고기 이동 정보
void FishUpdate2(DWORD _curTime);
DWORD FishRender1(DWORD _prevTime, DWORD _curTime, int _s);      // 물고기 그리기 정보 (_prevTime 값 반환)
DWORD FishRender2(DWORD _prevTime, DWORD _curTime, int _s);
void gotoXY(int _x, int _y);         // 커서 이동
void PrintSquare(int _type[][30], int _height, int _width);   // 맵정보와 크기를 입력받아 인터페이스를 만드는 함수
int PlarySkill(int _s);                  // 플라리 스킬
int PlarySingleAttack(int _a);                // 플라리 단일공격
void WholeSkillEffect(int _i);
void PrintWarning();            // 경고 출력
void CMDWindowsSetting();         // cmd 윈도우즈 창 관리
void ScreenCenter();            // cmd 윈도우즈 창 위치 중앙 고정
void XYConsole(int x, int y);      // cmd 윈도우즈 창 위치 임의 조정
int PrintPopup(int _height, int _width, int _s); // 가이드 창
void PopupLength(int _iPopupH, int _iPopupW, int _x, int _y);   // 헬퍼 인터페이스 길이 자동조절
void Exp(int _exp);         // 경험치바 관리
int PrintGameover(int _i, int _s);
void CountDown();
 
void menusound(int _s);      // 메뉴소리
void storesound(int _s);// 상점 bgm
void singlesound(int _s);
void continuesound(int _s);
void wholesound(int _s);    // 전체스킬소리
void titlesound(int _s); //타이틀 bgm
void gameexitsound(int _s); //게임 종료 소리
void gameoversound(int _s);// 게임오버 소리
void storystartsound(int _s); // 스토리 시작 bgm
void plaryappearsound(int _s); // 플라리 출현 bgm
void plaryspeaksound(int _s); // 플라리 말하는 중 bgm
void storyendsound(int _s); // 스토리 종료 bgm
void chapter2sound(int _s);// 챕터 2 시작 bgm
void ownerappearsound(int _s); // 주인등장
 
int main(void) // 메인
{
    DWORD prevTime1 = 0, deltaTime1 = 0, prevTime2 = 0, deltaTime2 = 0;
    int s = 3; // 소리 on off 관리, 3 : 모두 켜기 , 2 : 배경만 켜기, 1: 효과음만 켜기, 0:모두 끄기
    int i = 1, a = 0;// while문 동작여부, 단일공격 키
    DWORD prevTime = 0, curTime = 0;// 이전시간 현재시간 저장
    DWORD deltaTime = 0, elapsedTime = 0;// 현재시간과 이전시간의 차이, 흐른시간
    prevTime = timeGetTime(); // Miliseconds 단위로 시간 반환
    srand((unsigned int)time(0));
    CMDWindowsSetting();     // 초기 창 셋팅
    s = PrintTitle(s);        // 사운드 옵션 설정값 저장
    PrintPlayScreenInit(s);    // 플레이 초기화면
                            //CountDown();
    while (i)
    {
        curTime = timeGetTime();          // 현재시간 구하기
        deltaTime = curTime - prevTime; // 흐른시간 구하기
        elapsedTime += deltaTime; // 누적시간 구하기
 
        deltaTime1 = curTime - prevTime1;
        deltaTime2 = curTime - prevTime2;
 
        PrintPlayScreen(s); //게임 속도 조절
        PrintWarning();
 
        PrintTapInterface(s);
 
        a = PlarySingleAttack(a);// 단일공격
        if ((iDir == 0 || iDir == 1) && pull == 1) {
            gotoXY(PLARY_POSX - 6, PLARY_POSY); printf("    ");
            gotoXY(PLARY_POSX + 4, PLARY_POSY); printf("    ");
        }
        if (GetAsyncKeyState(VK_UP) && push == 1) iCell += iArtificiality; // 인공분열
 
        if (GetAsyncKeyState(0x48) && (iCell >= iWholeSkill))
        {
 
            prevTime1 = (unsigned long)(FishRender1(prevTime1, curTime, s));
            prevTime2 = (unsigned long)(FishRender2(prevTime2, curTime, s));
            PlarySkill(s);
 
        }
 
        prevTime1 = (unsigned long)(FishRender1(prevTime1, curTime, s));
        prevTime2 = (unsigned long)(FishRender2(prevTime2, curTime, s));
 
        // 물고기가 없는 빈공간에서도 스킬 사용 가능 하도록
        //if ((iDir == 0 || iDir == 1)) PlarySkill(s);
        //if (i1FishDie == 0 && iDir == 0 && g_arrFish[1].dir != (enum _DIR)L) PlarySkill(s);
        //if (i1FishDie == 0 && iDir != 0 && g_arrFish[1].dir != (enum _DIR)R) PlarySkill(s);
 
        // 상단 정보창 갱신
        gotoXY(77, 2);
        gotoXY(16, 3); printf("%d ", iLevel);
        gotoXY(31, 3); printf("%d   ", iCell);
        gotoXY(64, 3); printf("%d   ", iProtein);
 
        if (iCell <= 1)i = PrintGameover(i, s);// 게임오버 처리
    }
    return 0;
}
 
int PrintTitle(int _s)
{
    titlesound(_s);    // 게임 bgm 재생
    system("cls");
    // 특수문자 사용을 위한 설정
    _wsetlocale(LC_ALL, L"korean");
 
    // 애니메이션 정보를 담을 배열준비
    // 2차원 배열로 이루어진 이미지를 TOTAL_FRAME만큼 준비
    wchar_t arrFrames[TOTAL_FRAME][IMG_H][IMG_W];
 
 
 
    FILE* pFile = NULL;
    char szFileName[256];
    int i = 0, j = 0;
    // 애니메이션 프레임 개수만큼 반복
    for (i = 0; i < TOTAL_FRAME; ++i)
    {
        // 반복문 인덱스를 이용해서 파일경로 생성
        sprintf_s(szFileName, 256, "TV2\\Title_%02d.txt", i + 1);
        // 파일열기
        fopen_s(&pFile, szFileName, "r");
        if (pFile == NULL)
        {
            printf("!%s file open failed!\n", szFileName);
            return -1;
        }
 
        for (j = 0; j < IMG_H; ++j)
        {
            // 파일에서 이미지 정보 읽어오기
            fgetws(arrFrames[i][j], IMG_W, pFile);
        }
    }
 
    // Main Loop
    int curFrame = 0;                    // 현재 애니메이션 프레임
    float timeElapsed = 0.0f;           // 흐른시간
    DWORD lastTime = timeGetTime();        // 마지막에 기록된 시간
    while (1)
    {
        if (GetAsyncKeyState(VK_NUMPAD1))
        {
            menusound(_s);      // 효과음 함수
            fclose(pFile);
            PrintStoryQuest(_s);
            break;
        }
        else if (GetAsyncKeyState(VK_NUMPAD2))
        {
            _s = PrintSoundOptions(_s);
        }
        else if (GetAsyncKeyState(VK_NUMPAD3))
        {
            gameexitsound(_s); system("cls");
            PopupLength(2, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY); gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1); printf("게임을 종료합니다.");
            gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25);
            Sleep(1500); exit(0);
        }
        // 현재 프레임을 기준으로 이미지 그리기
        for (i = 0; i < IMG_H; ++i)
            wprintf(L"%s", arrFrames[curFrame][i]);
 
        DWORD curTime = timeGetTime();    //현재시간
                                          // timeGetTime은 밀리세컨드(millisecond, ms) 반환
                                          // 이 값에 0.001f을 곱해서 초 단위로 변환
        float timeDelta = (curTime - lastTime) * 0.001f;
        timeElapsed += timeDelta;// 변환된 시간을 누적
 
                                 // 누적된 시간이 프레임 전환 시간보다 크거나 같으면,
        if (timeElapsed >= 3.0f / TOTAL_FRAME)
        {
            ++curFrame;                    // 애니메이션 프레임 증가
                                           // 현재 프레임이 전체 프레임 개수를 넘으면, 0으로 초기화
            if (curFrame >= TOTAL_FRAME)
                curFrame = 0;
 
            timeElapsed = 0.0f;            // 흐른시간 초기화
        }
        else {// Sleep(10);
        }
        // 마지막에 기록된 시간을 갱신
        lastTime = curTime;
 
        // 화면 클리어
        gotoXY(0, 0);
        //system("cls");
    }
    return _s;
}
 
// 화면 전환시 초기 출력
int PrintPlayScreenInit(int _s)
{
    system("@cls||clear");
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);// 색깔 불러오기
    SetConsoleTextAttribute(hConsole, RESET_COLOR);// 색깔 설정하기    
    iArtificiality = 10;
    iSingleSkill = 1;
    iCountinuousSkill = 5;
    iWholeSkill = 350;
    printf("\n");
    PrintMap(MAP_HEIGHT, MAP_WIDTH);
    gotoXY(7, 25);
    SetConsoleTextAttribute(hConsole, TAB_COLOR);
    printf("\t │  Info  │");
    SetConsoleTextAttribute(hConsole, RESET_COLOR);
    printf(" │Cell Lab│\n");
    SetConsoleTextAttribute(hConsole, TAB_COLOR);
    printf("\t  ￣￣￣￣￣");
    SetConsoleTextAttribute(hConsole, RESET_COLOR);
    printf("   ￣￣￣￣￣\n");
    gotoXY(PLARY_POSX, PLARY_POSY);
    printf("○_"); gotoXY(5, 25); printf("\t");
    FishInit1();
    FishInit2();
    gotoXY(10, 23);
    printf("□□□□□□□□□□□□□□□□□□□□□□□□□□□□");
    gotoXY(43, 25); printf("EXP : %.1f / %.1f (%d%%)   ", fElapsedExp + fExtraElapesExp, fCurExpLimits, (int)((fBlock / 28) * 100));
    gotoXY(6, 27);
    PrintInfoTap();
    return _s;
}
 
int PrintPlayScreen(int _s) // 플레이화면 속도조절
{
 
    if (iTapSelect == 0)
    {
        InputKeyManager(PLARY_POSX, PLARY_POSY);
        Sleep(5);
    }
    else if (iTapSelect == 1 || iTapSelect == 2 || iTapSelect == 3)
    {
        system("cls");
        PrintMap(MAP_HEIGHT, MAP_WIDTH);
        PrintTapInterface(_s);
    }
    return _s;
}
 
int PrintStoryQuest(int _s)
{
    int i = 0, k = 0; // k : 스토리 모드를 틀었는지 판단
    PopupLength(5, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 1); printf("게임 설명 및 스토리를");
    gotoXY(POPUPSTART_POSX + 10, POPUPSTART_POSY + 2); printf("보시겠습니까?");
    while (1)
    {
        if (GetAsyncKeyState(VK_RETURN) && i == 0) // 스토리 모드 진행전 예 선택, 스토리 모드 출력
        {
            k = Chapter1(_s);
        };
        if (GetAsyncKeyState(VK_LEFT)) { --i; menusound(_s); }
        if (GetAsyncKeyState(VK_RIGHT)) { ++i; menusound(_s); }
        if (i > 1)i = 1;
        if (i < 0)i = 0;
        switch (i)
        {
        case 0:
            gotoXY(POPUPSTART_POSX + 8, POPUPSTART_POSY + 4); printf("▶예       아니오");
            gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25);
            system("pause"); break; 
        case 1:
            gotoXY(POPUPSTART_POSX + 8, POPUPSTART_POSY + 4); printf("  예     ▶아니오");
            gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25);
            system("pause");
        }
        if (GetAsyncKeyState(VK_RETURN) && k == 0 && i == 1)break; // 스토리 모드 진행전 아니오 선택, 게임 화면 출력
        if (GetAsyncKeyState(VK_RETURN) && k == 1 && i == 0)break; // 스토리 모드 진행후 예 선택, 게임화면 출력
        if (GetAsyncKeyState(VK_RETURN) && k == 1 && i == 1)main(); // 스토리 모드 진행후 아니오 선택, 타이틀 화면 출력
    }
    return _s;
}
 
int Chapter1(int _s)
{
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);// 색깔 불러오기
    SetConsoleTextAttribute(hConsole, RESET_COLOR);// 색깔 설정하기
    char cEnter;
    storystartsound(_s);
    system("cls");    Sleep(1200);
    PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);    Sleep(1200);
    gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 2); printf("스토리 모드");    Sleep(1400);
    gotoXY(POPUPSTART_POSX + 18, POPUPSTART_POSY + 2); printf("Chapter.1");    Sleep(1750);
    gotoXY(POPUPSTART_POSX + 10, POPUPSTART_POSY + 5); printf("플라리의 등장");
    gotoXY(POPUPSTART_POSX + 3, POPUPSTART_POSY + 6); printf("  ___○");    Sleep(500);
    gotoXY(POPUPSTART_POSX + 5, POPUPSTART_POSY + 6); printf("  _^_○");    Sleep(500);
    gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 6); printf("  ___○");    Sleep(500);
    gotoXY(POPUPSTART_POSX + 9, POPUPSTART_POSY + 6); printf("  _^_○");    Sleep(500);
    gotoXY(POPUPSTART_POSX + 11, POPUPSTART_POSY + 6); printf("   __○"); Sleep(7000);
    PrintPlayScreenInit(_s);
    gotoXY(PLARY_POSX, PLARY_POSY);    printf("   "); gotoXY(5, 25); printf("\t");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY - 1); printf("Chapter.1 플라리의 등장");
    plaryappearsound(_s);    Sleep(1050);
    WholeSkillEffect(115);
    gotoXY(PLARY_POSX, PLARY_POSY);    printf("○_"); gotoXY(5, 25); printf("\t");
    PrintStory(); gotoXY(STORYSTART_POSX + 22, STORYSTART_POSY + 25); printf("Enter >");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 25); printf("(1/3)");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 1); printf("앗! 깜짝이야!"); Sleep(1600);
    plaryspeaksound(_s); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 3); printf("넌 누구야?"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 5); printf("너도 혹시 날 괴롭히러 왔니?"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 7); printf("아니라구?"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 9); printf("믿긴 힘들지만 믿어줄게."); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 11); printf("..."); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 13); printf("아참! 내 소개부터 해줄게."); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 15); printf("안녕! 난 플라리야."); enter
        SetConsoleTextAttribute(hConsole, 12);
    gotoXY(STORYSTART_POSX - 2, STORYSTART_POSY + 10); printf("←");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 17); printf("여기는 내가 사는 어항속이지.");
    SetConsoleTextAttribute(hConsole, RESET_COLOR); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 19); printf("난 가만히 있으면 성장하지만"); enter
        SetConsoleTextAttribute(hConsole, 12);
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 21); printf("누군가 날 건드려도 성장해!");
    gotoXY(STORYSTART_POSX - 38, STORYSTART_POSY + 26);     printf("←");
    gotoXY(STORYSTART_POSX - 33, STORYSTART_POSY + 29); printf("→");
    SetConsoleTextAttribute(hConsole, RESET_COLOR); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 23); printf("인공 성장이 가능하다는 말씀!"); enter
        PrintStory(); gotoXY(STORYSTART_POSX + 22, STORYSTART_POSY + 25); printf("Enter >");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 25); printf("(2/3)");
    gotoXY(STORYSTART_POSX - 2, STORYSTART_POSY + 10); printf(" ");
    gotoXY(STORYSTART_POSX - 38, STORYSTART_POSY + 26); printf(" ");
    gotoXY(STORYSTART_POSX - 33, STORYSTART_POSY + 29); printf(" ");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 1); printf("요즘들어 부쩍 날 괴롭히는"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 3); printf("녀석들이 좀 생긴것 같아."); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 5); printf("바로 이렇게 생긴 놈들이야.");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 7); printf("           ▷◁>"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 9); printf("이녀석들은"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 11); printf("주인이 뿌린 밥을 먹을 땐"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 13); printf("몸 색이 이렇게 변하더라구!");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 15); printf("           ▶◀>"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 17); printf("그러다 너무 많이 먹으면"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 19); printf("죽어버린단 말이야?..."); enter
        SetConsoleTextAttribute(hConsole, 12);
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 21); printf("죽으면 단백질이 떨어져!");
    gotoXY(STORYSTART_POSX - 10, STORYSTART_POSY + 1); printf("↑");
    SetConsoleTextAttribute(hConsole, RESET_COLOR); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 23); printf("이거.. 좀 유용하더라구?"); enter
        PrintStory(); gotoXY(STORYSTART_POSX + 22, STORYSTART_POSY + 25); printf("Enter >");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 25); printf("(3/3)");
    gotoXY(STORYSTART_POSX - 10, STORYSTART_POSY + 1); printf(" ");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 1); printf("아무튼 난 내 몸집을"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 3); printf("좀 더 키워야 할 것 같아."); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 5); printf("물고기들이"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 7); printf("또 들이닥칠지도 모르거든."); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 11); printf("모아놓은 단백질로"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 13); printf("어떻게 더 강해질 수 있는지"); enter
        SetConsoleTextAttribute(hConsole, 12);
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 15); printf("연구 해봐야겠어!");
    gotoXY(STORYSTART_POSX - 43, STORYSTART_POSY + 23); printf("↑");
    SetConsoleTextAttribute(hConsole, RESET_COLOR); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 19); printf("고마워!"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 21); printf("내 얘기 들어줘서!"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 23); printf("나중에 또 볼 수 있으면 봐!");
    storyendsound(_s); enter
        int k = 0; // k : 스토리 모드를 모두 진행하기 전까지는 0
    k = Chapter2(_s);
    return k;
}
 
int Chapter2(int _s)
{
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);// 색깔 불러오기
    SetConsoleTextAttribute(hConsole, RESET_COLOR);// 색깔 설정하기
    char cEnter;
    chapter2sound(_s);
    system("cls");    Sleep(1200);
    PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);    Sleep(1200);
    gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 2); printf("스토리 모드");    Sleep(1400);
    gotoXY(POPUPSTART_POSX + 18, POPUPSTART_POSY + 2); printf("Chapter.2");    Sleep(1750);
    gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 5); printf("플라리가 너무 많아!");
    gotoXY(POPUPSTART_POSX + 5, POPUPSTART_POSY + 6); printf("_○");    Sleep(800);
    gotoXY(POPUPSTART_POSX + 10, POPUPSTART_POSY + 1); printf("○_");    Sleep(800);
    gotoXY(POPUPSTART_POSX + 24, POPUPSTART_POSY + 6); printf("_○");    Sleep(800);
    gotoXY(POPUPSTART_POSX + 20, POPUPSTART_POSY + 3); printf("○_");    Sleep(800);
    gotoXY(POPUPSTART_POSX + 12, POPUPSTART_POSY + 7); printf("_○"); Sleep(2000);
    PrintPlayScreenInit(_s);
    gotoXY(PLARY_POSX - 20, PLARY_POSY + 6);    printf("○_");
    gotoXY(PLARY_POSX + 18, PLARY_POSY - 5);    printf("○_");
    gotoXY(PLARY_POSX + 8, PLARY_POSY - 7);    printf("_○");
    gotoXY(PLARY_POSX - 8, PLARY_POSY + 2);    printf("○_");
    gotoXY(PLARY_POSX + 3, PLARY_POSY + 4);    printf("_○");
    gotoXY(PLARY_POSX + 12, PLARY_POSY + 3);    printf("○_");
    gotoXY(PLARY_POSX - 14, PLARY_POSY - 2);    printf("_○");
    ownerappearsound(_s);
    PrintStory(); gotoXY(STORYSTART_POSX + 22, STORYSTART_POSY + 25); printf("Enter >");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY - 1); printf("Chapter.2 플라리가 너무 많아!");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 25); printf("(1/1)");
    Sleep(2000);
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 1); printf("플라리 :");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 3); printf("헉! 저기 주인이 오고있어!"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 5); printf("어서 몸을 피해야해!"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 7); printf("주인 :");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 9); printf("어디 우리 물고기들이"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 11); printf("잘 있는지 한번 볼까?"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 13); printf("!!!!"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 15); printf("아니! 이 징그러운 플라리들!"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 17); printf("안되겠다! 물고기들을 무한정"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 19); printf("풀어 다 말살 시켜버리겠다!"); enter
        gotoXY(PLARY_POSX - 20, PLARY_POSY + 6);    printf("○_ <▷◁"); enter
        gotoXY(PLARY_POSX + 18, PLARY_POSY - 5);    printf("○_<▶◀");
    gotoXY(PLARY_POSX + 2, PLARY_POSY - 7);    printf("▷◁> _○");
    gotoXY(PLARY_POSX - 8, PLARY_POSY + 2);    printf("○_  <▷◁"); enter
        gotoXY(PLARY_POSX - 3, PLARY_POSY + 4);    printf("▷◁> _○");
    gotoXY(PLARY_POSX + 12, PLARY_POSY + 3);    printf("○_ <▶◀");
    gotoXY(PLARY_POSX - 20, PLARY_POSY - 2);    printf("▶◀> _○"); enter
        gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 21); printf("플라리 :");
    gotoXY(STORYSTART_POSX + 2, STORYSTART_POSY + 23); printf("안돼!! 나 좀 도와줘!");
    storyendsound(_s); enter
        PopupLength(8, POPUP_WIDTH, 39, 16);
    gotoXY(47, 18); printf("게임을 진행합니다. ");
    gotoXY(44, 19); printf("하단 INFO 탭의 단축키를");
    gotoXY(48, 20); printf("확인해 주세요.");
    int k = 1; // 스토리 모드를 모두 진행
    return k;
}
 
// 어항(플레이 맵)을 그리는 함수
void PrintMap(int _height, int _width)
{
    printf("\n\n\t  LEVEL %d\t CELLS %d\t EXP %.1f   \tPROTEIN %d\t\n", iLevel, iCell, fTotalExp, iProtein);
    printf("\t──────────────────────────────\n");
    printf("\t  [STAGE %d]\tSCORE  %d", 1, 0);
    PrintSquare(g_arrMap, MAP_HEIGHT, MAP_WIDTH);
}
 
// 탭 인터페이스를 그리는 함수
void PrintTap(int _height, int _width)
{
    PrintSquare(g_arrTap, TAP_HEIGHT, TAP_WIDTH);
}
 
// 스토리 인터페이스를 그리는 함수
void PrintStory()
{
    PopupLength(STORY_HEIGHT, STORY_WIDTH, STORYSTART_POSX, STORYSTART_POSY);
}
 
// 맵정보와 크기를 입력받아 인터페이스를 만드는 함수
void PrintSquare(int _type[][30], int _height, int _width)
{
    int i = 0, j = 0;
    for (i = 0; i <_height; ++i)
    {
        printf("\t");
        for (j = 0; j < _width; ++j)
        {
            if (_type[i][j] == 0)
                printf("  ");
            else if (_type[i][j] == 1)
                printf("│");
            else if (_type[i][j] == 2)
                printf("─");
            else if (_type[i][j] == 3)
                printf("┌");
            else if (_type[i][j] == 4)
                printf("┐");
            else if (_type[i][j] == 5)
                printf("└");
            else if (_type[i][j] == 6)
                printf("┘");
        }
        puts("");
    }
}
 
// 탭 모양 및 색깔을 그리는 함수
int PrintTapInterface(int _s)
{
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    SetConsoleTextAttribute(hConsole, RESET_COLOR);
 
    if (GetAsyncKeyState(VK_TAB))
    {
        system("cls");
        if (iTapSelect < TheNum_MENU - 2)
        {
            menusound(_s);
            ++iTapSelect;
        }
        else  iTapSelect = 0;
 
        switch (iTapSelect)
        {
        case 0:
            printf("\n");
            PrintMap(MAP_HEIGHT, MAP_WIDTH);
            gotoXY(10, 23);
            printf("□□□□□□□□□□□□□□□□□□□□□□□□□□□□");
            gotoXY(7, 25);
            SetConsoleTextAttribute(hConsole, TAB_COLOR);
            printf("\t │  Info  │");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            printf(" │Cell Lab│\n");
            SetConsoleTextAttribute(hConsole, TAB_COLOR);
            printf("\t  ￣￣￣￣￣");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            printf("   ￣￣￣￣￣\n");
            gotoXY(PLARY_POSX, PLARY_POSY);
            // 플라리 바라보고 있던 방향정보 가져오기
            if (iDir == 0) {
                printf("○_"); gotoXY(5, 25); printf(" ");
            }
            else if (iDir == 1) {
                printf("_○"); gotoXY(5, 25); printf(" ");
            }
            gotoXY(43, 25); printf("EXP : %.1f / %.1f (%d%%)   ", fElapsedExp + fExtraElapesExp, fCurExpLimits, (int)((fBlock / 28) * 100));
 
            gotoXY(6, 27);
            PrintInfoTap(); break;
        case 1:
            printf("\n");
            PrintMap(MAP_HEIGHT, MAP_WIDTH);
            printf("\t │  Info  │");
            SetConsoleTextAttribute(hConsole, TAB_COLOR);
            printf(" │Cell Lab│\n");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            printf("\t  ￣￣￣￣￣");
            SetConsoleTextAttribute(hConsole, TAB_COLOR);
            printf("   ￣￣￣￣￣\n");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            PrintCellLabTap(_s);
            menusound(_s); CountDown(); 
 
            // 여기부터 함수 간소화 필요
            gotoXY(0, 0);
            system("cls");
            printf("\n");
            PrintMap(MAP_HEIGHT, MAP_WIDTH);
            gotoXY(10, 23);
            printf("□□□□□□□□□□□□□□□□□□□□□□□□□□□□");
            gotoXY(7, 25);
            SetConsoleTextAttribute(hConsole, TAB_COLOR);
            printf("\t │  Info  │");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            printf(" │Cell Lab│\n");
            SetConsoleTextAttribute(hConsole, TAB_COLOR);
            printf("\t  ￣￣￣￣￣");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            printf("   ￣￣￣￣￣\n");
            gotoXY(PLARY_POSX, PLARY_POSY);
            // 플라리 바라보고 있던 방향정보 가져오기
            if (iDir == 0) {
                printf("○_"); gotoXY(5, 25); printf(" ");
            }
            else if (iDir == 1) {
                printf("_○"); gotoXY(5, 25); printf(" ");
            }
            gotoXY(43, 25); printf("EXP : %.1f / %.1f (%d%%)   ", fElapsedExp + fExtraElapesExp, fCurExpLimits, (int)((fBlock / 28) * 100));
 
            gotoXY(6, 27);
            PrintInfoTap(); break; 
 
        }
    }
 
 
    return _s;
}
 
// 플레이시에 플라리 방향 처리
void InputKeyManager(int _x, int _y)
{
    iTapSelect = 0;
    if (iDir == 0) {
        gotoXY(_x, _y); printf("○_"); gotoXY(5, 25); printf(" ");
    }
    else if (iDir == 1) {
        gotoXY(_x, _y); printf("_○"); gotoXY(5, 25); printf(" ");
    }
    if (GetAsyncKeyState(VK_LEFT))
    {
        iDir = 0;
        gotoXY(_x, _y);
        printf("○_"); gotoXY(5, 25); printf(" ");
    }
    if (GetAsyncKeyState(VK_RIGHT))
    {
        iDir = 1;
        gotoXY(_x, _y);
        printf("_○"); gotoXY(5, 25); printf(" ");
    }
}
 
void PrintInfoTap() // 인포 탭
{
    printf("\t   =======================  Info  =======================\n");
    PrintTap(TAP_HEIGHT, TAP_WIDTH);
    gotoXY(10, 29); printf("⊙ 초당 세포증가 :\t\t단일공격 : A Key");
    gotoXY(10, 30); printf("⊙ 인공 세포분열 : %d\t\t연속공격 : Space bar", iArtificiality);
    gotoXY(10, 31); printf("               \t\t전체공격 : H Key");
    gotoXY(10, 32); printf("⊙ 세포 소모량");
    gotoXY(10, 33); printf("   - 단일공격 : %d\t\t인공분열 : ↑", iSingleSkill);
    gotoXY(10, 34); printf("   - 연속공격 : %d\t\t왼    쪽 : ←", iCountinuousSkill);
    gotoXY(10, 35); printf("   - 전체공격 : %d\t\t오 른 쪽 : →", iWholeSkill);
    gotoXY(10, 36); printf("               \t\t메뉴선택 : TAB Key");
}
int PrintCellLabTap(int _s) // 상점 탭
{
    int i = 0;
    printf("\t   ======================= CellLab ======================\n");
    storesound(_s);
    PrintTap(TAP_HEIGHT, TAP_WIDTH);
    PopupLength(3, POPUP_WIDTH, 11, 8);
    gotoXY(13, 7); printf("_○");
    gotoXY(16, 9); printf("여기서 단백질을 이용해!");
    gotoXY(15, 10); printf("여기, 내 정보를 띄워줄게!");
    gotoXY(28, 13); printf("-----플라리 정보-----");
    gotoXY(15, 15); printf("⊙ 인공 세포분열 : %d", iArtificiality);
    gotoXY(15, 17); printf("⊙ 현재 경험치   : %.2f / %.2f (%d%%)", fElapsedExp + fExtraElapesExp, fCurExpLimits, (int)((fBlock / 28) * 100));
    gotoXY(15, 19); printf("⊙ 스킬 세포 소모량");
    gotoXY(15, 20); printf("   - 단일공격    : %d", iSingleSkill);
    gotoXY(15, 21); printf("   - 연속공격    : %d", iCountinuousSkill);
    gotoXY(15, 22); printf("   - 전체공격    : %d", iWholeSkill);
    iTapSelect = 0;
    while (1)
    { // 상점 메뉴선택 시작
 
 
        switch (i)
        {
        case 0:
            gotoXY(12, 29); printf("▶인공 세포분열 연구");
            gotoXY(12, 31); printf("  스킬 효율성 연구");
            gotoXY(12, 33); printf("  단백질 변환 연구");
            gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause"); break;
        case 1:
            gotoXY(12, 29); printf("  인공 세포분열 연구");
            gotoXY(12, 31); printf("▶스킬 효율성 연구");
            gotoXY(12, 33); printf("  단백질 변환 연구");
            gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause"); break;
        case 2:
            gotoXY(12, 29); printf("  인공 세포분열 연구");
            gotoXY(12, 31); printf("  스킬 효율성 연구");
            gotoXY(12, 33); printf("▶단백질 변환 연구");
            gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause"); break;
        }
        if (GetAsyncKeyState(VK_UP))    --i;
        if (GetAsyncKeyState(VK_DOWN))    ++i;
        if (GetAsyncKeyState(VK_TAB))    {        iTapSelect = -1; break;    }
 
        if (i > 2) i = 0;
        if (i < 0) i = 2;
        // 인공세포분열 연구 시작
        if (GetAsyncKeyState(VK_RETURN) && i == 0)
        {
            int k = 0, j = 0, l = 0;
            while (1) {// 인공세포분열 상점 연구 while문 시작
                if (GetAsyncKeyState(VK_UP)) --k;
                if (GetAsyncKeyState(VK_DOWN)) ++k;
                if (k > 1) k = 1;
                if (k < 0) k = 0;
                switch (k)
                {
                    // 수량 수동입력 시작
                case 0:
                    PopupLength(10, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 1); printf(" 1 증가 / 100 단백질");
                    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 3); printf("▶수량 입력");
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 4); printf("◁                 ▶");
                    gotoXY(POPUPSTART_POSX + 16, POPUPSTART_POSY + 4); printf("%d  ", 0);
                    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 6); printf("  최대치 구매");
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 7); printf("인공증가 : %d개", (int)(iProtein / 100));
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 8); printf("비용 : %.0f단백질", (double)(iProtein / 100) * 100);
 
                    while (1)
                    {
                        if (GetAsyncKeyState(VK_RIGHT)) { ++j; gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 4); printf("◁                 ▶");}
                        if (GetAsyncKeyState(VK_LEFT)) { --j; gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 4); printf("◀                 ▷");}
                        if (j < 1)
                        {
                            j = 0; gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 4); printf("◁                 ▶");
                        }
                        if ((j) * 100 > iProtein)
                        {
                            --j;
                            gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 4); printf("◀                 ▷");
                        }
                        gotoXY(POPUPSTART_POSX + 16, POPUPSTART_POSY + 4); printf("%d  ", j);
                        gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
                        if (GetAsyncKeyState(VK_UP)) { --k; break; }
                        if (GetAsyncKeyState(VK_DOWN)) { ++k; break; }
                        if (GetAsyncKeyState(VK_RETURN)) {
                            iArtificiality += j; iProtein -= j * 100; iTapSelect = 0;
                            gotoXY(15, 15); printf("⊙ 인공 세포분열 : %d", iArtificiality);
                            gotoXY(64, 3); printf("%d   ", iProtein); j = 0; gotoXY(POPUPSTART_POSX + 16, POPUPSTART_POSY + 4); printf("%d  ", j);    break;
                        }
                        //if (GetAsyncKeyState(VK_ESCAPE)) break;
                    }
                    break;// 수량 수동입력 종료
 
                          //수량 최대치 입력 시작
                case 1:
                    PopupLength(10, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 1); printf(" 1 증가 / 100 단백질");
                    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 3); printf("  수량 입력");
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 4); printf("◁                 ▶");
                    gotoXY(POPUPSTART_POSX + 16, POPUPSTART_POSY + 4); printf("%d  ", 0);
                    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 6); printf("▶최대치 구매");
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 7); printf("인공증가 : %d개", (int)(iProtein / 100));
                    gotoXY(POPUPSTART_POSX + 6, POPUPSTART_POSY + 8); printf("비용 : %.0f단백질", (double)(iProtein / 100) * 100);
                    while (1)
                    {
                        if (GetAsyncKeyState(VK_UP)) { --k; break; }
                        if (GetAsyncKeyState(VK_DOWN)) { ++k; break; }
                        if (GetAsyncKeyState(VK_RETURN))
                        {
                            iArtificiality += (int)(iProtein / 100); iProtein -= (int)(iProtein / 100) * 100; iTapSelect = 0;
                            gotoXY(15, 15); printf("⊙ 인공 세포분열 : %d", iArtificiality);
                            gotoXY(64, 3); printf("%d   ", iProtein); break;
                        }
                        gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
 
                    }break;// 수량 최대치 입력 종료
 
                }// 스위치 종료
                if (GetAsyncKeyState(VK_RETURN))break;
            }//인공세포분열 상점 연구 while문 종료
 
        }// 인공세포분열 연구 종료
        if (GetAsyncKeyState(VK_RETURN))break;
        if (iTapSelect == -1) break;
    }// 상점 메뉴 선택 종료
    iTapSelect = 0;
    return _s;
}
void PrintSkillTap() // 스킬 탭
{
    printf("\t   =======================  Skill  ======================\n");
    PrintTap(TAP_HEIGHT, TAP_WIDTH); // 임시삭제
}
 
// 물고기1 초기 정보
void FishInit1()
{
    int i = 1;
    g_arrFish[i].fPosX = 11;
    g_arrFish[i].fPosY = 14;
    g_arrFish[i].dSpeed = 0.02;
    g_arrFish[i].dir = (enum _DIR)R;
}
// 물고기2 초기 정보
void FishInit2()
{
    int i = 2;
    g_arrFish[i].fPosX = 61;
    g_arrFish[i].fPosY = 14;
    g_arrFish[i].dSpeed = 0.02;
    g_arrFish[i].dir = (enum _DIR)L;
}
// 물고기1 이동 정보
void FishUpdate1(DWORD _curTime)
{
    int i = 1;
    g_arrFish[i].fPosX += (float)(g_arrFish[i].dSpeed*g_arrDir[g_arrFish[i].dir].fX);
    g_arrFish[i].fPosY += (float)(g_arrFish[i].dSpeed*g_arrDir[g_arrFish[i].dir].fY);
    if (g_arrFish[i].fPosX >= 30) // 물고기 근접시 처리
    {
        iFishNear1 = 1;
        g_arrFish[i].fPosX = 30;
        iCell -= 24;
        gotoXY(30, 14);
        printf(" ▶◀>");
        g_arrFish[i].fHunger += 1;
    }
}
// 물고기2 이동 정보
void FishUpdate2(DWORD _curTime)
{
    int i = 2;
    g_arrFish[i].fPosX += (float)(g_arrFish[i].dSpeed*g_arrDir[g_arrFish[i].dir].fX);
    g_arrFish[i].fPosY += (float)(g_arrFish[i].dSpeed*g_arrDir[g_arrFish[i].dir].fY);
    if (g_arrFish[i].fPosX <= 42) // 물고기 근접시 처리
    {
        iFishNear2 = 1;
        g_arrFish[i].fPosX = 42;
        iCell -= 24;
        gotoXY(42, 14);
        printf(" <▶◀");
        g_arrFish[i].fHunger += 1;
    }
}
 
// 물고기1 그리기 정보
DWORD FishRender1(DWORD _prevTime, DWORD _curTime, int _s)
{
    int i = 1;
    DWORD deltaTime1 = _curTime - _prevTime;
    if (i1FishDie == 0) // 피쉬다이가 0인경우
    {
        _prevTime = _curTime; // 현재시간을 계속 저장
        FishUpdate1(_curTime);
        gotoXY(
            (int)g_arrFish[i].fPosX,
            (int)g_arrFish[i].fPosY);
        // 물고기 배고픔이 다 차기 전
        if (g_arrFish[i].fHunger < 5)
        {
            if (GetAsyncKeyState(VK_SPACE) && iDir == 0 && (iCell >= iCountinuousSkill))
            {
                printf(" ▶◀>");
                PlarySkill(_s);
                g_arrFish[i].fHunger += iCellUseUp;
            }
            else if (push == 1 && GetAsyncKeyState(0x41) && iDir == 0 && (iCell >= iSingleSkill))
            {
                printf(" ▶◀>");
                PlarySkill(_s);
                g_arrFish[i].fHunger += iCellUseUp;
            }
            else if (GetAsyncKeyState(0x48) && (iCell >= iWholeSkill))
            {
                g_arrFish[i].fHunger += iCellUseUp;
                printf(" ▶◀>");
            }
            else
                printf(" ▷◁>");
        }
 
        else  // 물고기 배고픔이 다 찬 후
        {
            printf("      ");
            FishInit1();
            if (iFishNear1 == 0)
            {
                Exp(16);
                iProtein += 82;
            }
            else
            {
                Exp(1);
                iProtein += 3;
                iFishNear1 = 0;
            }
            g_arrFish[i].fHunger = 0;
            i1FishDie = 1;
        }
 
    }
    if (deltaTime1 / 1000.0f >= 2.0f&&i1FishDie == 1) // 피쉬렌더에서 피쉬다이가 1로 체크 될 때
    { // 일정 시간을 카운팅후 피쉬다이를 다시 0으로 풀어줌
        i1FishDie = 0;
        printf("      ");
    }
    return _prevTime;
}
// 물고기2 그리기 정보
DWORD FishRender2(DWORD _prevTime, DWORD _curTime, int _s)
{
    int i = 2;
    DWORD deltaTime2 = _curTime - _prevTime;
    if (i2FishDie == 0) // 피쉬다이가 0인경우
    {
        _prevTime = _curTime; // 현재시간을 계속 저장
        FishUpdate2(_curTime);
        gotoXY(
            (int)g_arrFish[i].fPosX,
            (int)g_arrFish[i].fPosY);
        if (g_arrFish[i].fHunger < 5)// 물고기 배고픔이 다 차기 전
        {
            if (GetAsyncKeyState(VK_SPACE) && iDir == 1 && (iCell >= iCountinuousSkill))
            {
                printf("<▶◀ ");
                PlarySkill(_s);
                g_arrFish[i].fHunger += iCellUseUp;
            }
            else if (push == 1 && GetAsyncKeyState(0x41) && iDir == 1 && (iCell >= iSingleSkill))
            {
                printf("<▶◀ ");
                PlarySkill(_s);
                g_arrFish[i].fHunger += iCellUseUp;
            }
            else if (GetAsyncKeyState(0x48) && (iCell >= iWholeSkill))
            {
                g_arrFish[i].fHunger += iCellUseUp;
                printf("<▶◀ ");
            }
            else
                printf("<▷◁");
        }
 
        else  // 물고기 배고픔이 다 찬 후
        {
            printf("      ");
            FishInit2();
            if (iFishNear2 == 0)
            {
                Exp(16);
                iProtein += 82;
            }
            else
            {
                Exp(1);
                iProtein += 3;
                iFishNear2 = 0;
            }
            g_arrFish[i].fHunger = 0;
            i2FishDie = 1;
        }
 
    }
    if (deltaTime2 / 1000.0f >= 2.0f&&i2FishDie == 1) // 피쉬렌더에서 피쉬다이가 1로 체크 될 때
    { // 일정 시간을 카운팅후 피쉬다이를 다시 0으로 풀어줌
        i2FishDie = 0;
        printf("      ");
    }
    return _prevTime;
}
 
// 커서 이동
void gotoXY(int _x, int _y)
{
    COORD pos = { _x,_y };
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), pos);
}
 
// 플라리 스킬
int PlarySkill(int _s)
{
    if (GetAsyncKeyState(0x41) && iCell > iSingleSkill)// 단일공격
    {
        iCellUseUp = iSingleSkill;
        if (iDir == 0 && push == 1)
        {
            singlesound(_s);
            gotoXY(PLARY_POSX - 7, PLARY_POSY); printf("º---"); iCell -= iSingleSkill;
        }
        else if (iDir == 1 && push == 1)
        {
            singlesound(_s);
            gotoXY(PLARY_POSX + 4, PLARY_POSY); printf("---º"); iCell -= iSingleSkill;
        }
    }
    if (GetAsyncKeyState(VK_SPACE) && iCell>iCountinuousSkill)  // 연사 공격
    {
        continuesound(_s);
        iCellUseUp = iCountinuousSkill;
        if (iDir == 0) // 왼쪽방향 이펙트
        {
            gotoXY(PLARY_POSX - 7, PLARY_POSY); printf("º---");
            Sleep(5);
            gotoXY(PLARY_POSX - 7, PLARY_POSY); printf("º--   ");
            Sleep(5);
            gotoXY(PLARY_POSX - 8, PLARY_POSY); printf("º-  ");
            Sleep(5);
            gotoXY(PLARY_POSX - 9, PLARY_POSY); printf("º  ");
            iCell -= iCellUseUp;
        }
        else if (iDir == 1) // 오른쪽방향 이펙트
        {
            gotoXY(PLARY_POSX + 4, PLARY_POSY); printf("---º");
            Sleep(5);
            gotoXY(PLARY_POSX + 4, PLARY_POSY); printf("  --º");
            Sleep(5);
            gotoXY(PLARY_POSX + 4, PLARY_POSY); printf("     º");
            Sleep(5);
            gotoXY(PLARY_POSX + 4, PLARY_POSY); printf("      º");
            iCell -= iCellUseUp;
        }
        Sleep(30);
        gotoXY(PLARY_POSX - 16, PLARY_POSY); printf("　　　　");
        gotoXY(PLARY_POSX + 3, PLARY_POSY); printf("　　 　　");
    }
    if (GetAsyncKeyState(0x48) && iCell>iWholeSkill) // 전체 공격
    {
        wholesound(_s);
        iCellUseUp = iWholeSkill;
        iCell -= iCellUseUp;
        WholeSkillEffect(50);
    }
    return _s;
}
 
void WholeSkillEffect(int _i)
{
    int i = 5;
    for (_i; _i > 0; ) // 세포 충전 이펙트
    {
        gotoXY(PLARY_POSX - (2 + i), PLARY_POSY); printf("º"); Sleep(_i);//0
        gotoXY(PLARY_POSX - (i), PLARY_POSY - i + 1); printf("º"); Sleep(_i);//1
        gotoXY(PLARY_POSX, PLARY_POSY - i); printf("º");//2
        gotoXY(PLARY_POSX - (2 + i), PLARY_POSY); printf(" "); Sleep(_i);//0
        gotoXY(PLARY_POSX + i, PLARY_POSY - i + 1); printf("º");//3
        gotoXY(PLARY_POSX - (i), PLARY_POSY - i + 1); printf(" "); Sleep(_i);//1
        gotoXY(PLARY_POSX + 2 + i, PLARY_POSY); printf("º");//4
        gotoXY(PLARY_POSX, PLARY_POSY - i); printf(" "); Sleep(_i);//2
        gotoXY(PLARY_POSX + i, PLARY_POSY + i - 1); printf("º");//5
        gotoXY(PLARY_POSX + i, PLARY_POSY - i + 1); printf(" "); Sleep(_i);//3
        gotoXY(PLARY_POSX, PLARY_POSY + i); printf("º");//6
        gotoXY(PLARY_POSX + 3 + i, PLARY_POSY); printf(" "); Sleep(_i);//4
        gotoXY(PLARY_POSX - (i), PLARY_POSY + i - 1); printf("º");//7
        gotoXY(PLARY_POSX + i, PLARY_POSY + i - 1); printf(" "); Sleep(_i);//5
        gotoXY(PLARY_POSX, PLARY_POSY + i); printf(" "); Sleep(_i);//6
        gotoXY(PLARY_POSX - (i), PLARY_POSY + i - 1); printf(" ");//7
        _i -= 11;
        --i;
        if (i < 2) i = 2;
    }
    for (int i = 1; i < 5; ++i) // 세포 발사 이펙트
    {
        gotoXY(PLARY_POSX, PLARY_POSY + ((i * 2))); printf("º");
        gotoXY(PLARY_POSX, PLARY_POSY - ((i * 2))); printf("º");
        gotoXY(PLARY_POSX + (i * 3) - 1, PLARY_POSY + (i * 2) - 1); printf("º");
        gotoXY(PLARY_POSX + (i * 3) - 1, PLARY_POSY - ((i * 2) - 1)); printf("º");
        gotoXY(PLARY_POSX - ((i * 3) - 1), PLARY_POSY + (i * 2) - 1); printf("º");
        gotoXY(PLARY_POSX - ((i * 3) - 1), PLARY_POSY - ((i * 2) - 1)); printf("º");
        gotoXY(PLARY_POSX + (i * 3) + i, PLARY_POSY); printf("º  ");
        gotoXY(PLARY_POSX - ((i * 3) + i), PLARY_POSY); printf("º  ");
        Sleep(15);
    }
    for (int i = 1; i < 5; ++i) // 세포 잔상 지우기 이펙트
    {
        gotoXY(PLARY_POSX, PLARY_POSY + ((i * 2))); printf(" ");
        gotoXY(PLARY_POSX, PLARY_POSY - ((i * 2))); printf(" ");
        gotoXY(PLARY_POSX + (i * 3) - 1, PLARY_POSY + (i * 2) - 1); printf(" ");
        gotoXY(PLARY_POSX + (i * 3) - 1, PLARY_POSY - ((i * 2) - 1)); printf(" ");
        gotoXY(PLARY_POSX - ((i * 3) - 1), PLARY_POSY + (i * 2) - 1); printf(" ");
        gotoXY(PLARY_POSX - ((i * 3) - 1), PLARY_POSY - ((i * 2) - 1)); printf(" ");
        gotoXY(PLARY_POSX + (i * 3) + i, PLARY_POSY); printf("  ");
        gotoXY(PLARY_POSX - ((i * 3) + i), PLARY_POSY); printf("  ");
        Sleep(20);
    }
}
 
int PlarySingleAttack(int _a) // 단일공격
{
    curt = 0;
    if (GetAsyncKeyState(0x41))  curt = 1; // A키
    if (GetAsyncKeyState(VK_UP))  curt = 1; // 화살표 위쪽
 
    push = (prev ^ curt) & curt;
    pull = (prev ^ curt) & prev;
    prev = curt;
    _a = 1;
    return _a;
}
 
void PrintWarning()// 경고 출력
{
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    if (iCell >= 0)
    {
        //iCell += 1;
        if (iCell >= iCellUseUp * 35)
        {
            gotoXY(50, 5);
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
            printf("                  ");
        }
        else if (iCell <= iCellUseUp * 35)
        {
            gotoXY(50, 5);
            SetConsoleTextAttribute(hConsole, 12);
            printf("경고! 세포 부족!");
            SetConsoleTextAttribute(hConsole, RESET_COLOR);
        }
    }
    else
        iCell = 0;
}
 
// 현재 해상도 정보를 불러와 cmd 창 위치 중앙고정
void ScreenCenter()
{
    HWND hWnd_console;
    HWND hWnd_desktop;
    RECT rect_console = { 0, };
    RECT rect_desktop = { 0, };
    int x, y;
 
    hWnd_console = GetConsoleWindow();
    hWnd_desktop = GetDesktopWindow();
 
    GetWindowRect(hWnd_desktop, &rect_desktop);
    GetWindowRect(hWnd_console, &rect_console);
 
    x = (rect_desktop.left + rect_desktop.right - rect_console.right + rect_console.left) / 2;
    y = (rect_desktop.top + rect_desktop.bottom - rect_console.bottom + rect_console.top) / 2;
 
    SetWindowPos(hWnd_console, NULL, x, y, 0, 0, SWP_NOSIZE | SWP_NOZORDER | SWP_NOACTIVATE);
}
 
// cmd 윈도우즈 창 위치 임의 조정
void XYConsole(int x, int y)
{
    HWND hWnd_console;
 
    hWnd_console = GetConsoleWindow();
    SetWindowPos(hWnd_console, NULL, x, y, 0, 0, SWP_NOSIZE | SWP_NOZORDER | SWP_NOACTIVATE);
}
 
// cmd 윈도우즈 창 관리
void CMDWindowsSetting()
{
    system("mode con: cols=109 lines=45");// cmd 윈도우즈 창 크기 조절
                                         ScreenCenter();   // 화면 중앙 위치시키기
    //XYConsole(100, 100); // 화면위치 임의 조정
}
 
// 가이드 창
int PrintPopup(int _height, int _width, int _s)
{
    menusound(_s);
    gotoXY(10, 1);
    printf("Game Start Guide : Press F1");
    gotoXY(POPUPSTART_POSX + 8, POPUPSTART_POSY + 1);
    printf("Game Start Guide!\n");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 3);
    printf("Left : Q Right : W");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 5);
    printf("Attack : Space");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 7);
    printf("Whole Attack : H");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 9);
    printf("Tab windows : TAB");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 11);
    printf("원거리 공격시엔 증가하는");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 12);
    printf("경험치와 돈이 많지만");
    gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 13);
    printf("물고기 근접후엔 적게받음");
    PopupLength(15, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
    return _s;
}
 
// 팝업 인터페이스 길이 자동조절
void PopupLength(int _iPopupH, int _iPopupW, int _x, int _y)
{
    int i = 0, j = 0;
    for (i; i < _iPopupH; ++i)
    {
        for (j = 0; j < _iPopupW; ++j)
        {
            gotoXY(j * 2 + _x, i + _y);
 
            if (*(g_arrPopup[i] + j) == 0)
                printf("  ");
            else if (*(g_arrPopup[i] + j) == 1)
                printf("│");
            else if (*(g_arrPopup[i] + j) == 2)
                printf("─");
            else if (*(g_arrPopup[i] + j) == 3)
                printf("┌");
            else if (*(g_arrPopup[i] + j) == 4)
                printf("┐");
        }
        puts("");
    }
    for (j = 0; j < _iPopupW; ++j)
    {
        gotoXY(j * 2 + _x, i + _y);
        if (*(g_arrPopup[24] + j) == 2)
            printf("─");
        else if (*(g_arrPopup[24] + j) == 5)
            printf("└");
        else if (*(g_arrPopup[24] + j) == 6)
            printf("┘");
    }
}
 
// 경험치바 관리
void Exp(int _exp)
{
    int i = 0;
    gotoXY(10, 23);
    printf("□□□□□□□□□□□□□□□□□□□□□□□□□□□□");
    fCurExpLimits = (float)(iLevel*1.1 + fPrevExpLimits*0.9 + 30); // 현재 레벨 경험치 상한선
    fElapsedExp += _exp + fExtraElapesExp;
    fBlock = (((fElapsedExp) / fCurExpLimits) * 28);
    for (iExpFulling; i < fBlock; ++iExpFulling) // 현재 레벨의 블록을 채워 줌
    {
        if (fBlock >= 28) fBlock = 28;
        gotoXY(10 + iExpFulling * 2, 23);
        printf("■");
        ++i;
    }
    fExtraElapesExp = 0;
    if (fElapsedExp >= fCurExpLimits) // 레벨업시 남은 경험치 블록을 채워 줌
    {
        fLeftExp = fElapsedExp - fCurExpLimits;
        fExtraElapesExp = fLeftExp;
        fPrevExpLimits = fCurExpLimits;
        fCurExpLimits = (float)((iLevel + 1) * 1.1 + fPrevExpLimits*0.9 + 30); // 다음 레벨 경험치 상한선
        fBlock = (((fLeftExp) / fCurExpLimits) * 28);
        ++iLevel;
        gotoXY(10, 23);
        printf("□□□□□□□□□□□□□□□□□□□□□□□□□□□□");
        fElapsedExp = 0;
        iExpFulling = 0;
        for (iExpFulling; iExpFulling < fBlock; ++iExpFulling)
        {
            gotoXY(10 + iExpFulling * 2, 23);
            printf("■");
        }
        fLeftExp = 0;
    }
    iExpFulling = 0;
    fCurExpLimits = (float)((iLevel) * 1.1 + fPrevExpLimits*0.9 + 30); // 현재 레벨 경험치 상한선
    fTotalExp += _exp;
    gotoXY(45, 3); printf("%.1f", fTotalExp);
    gotoXY(43, 25); printf("EXP : %.1f / %.1f (%d%%)   ", fElapsedExp + fExtraElapesExp, fCurExpLimits, (int)((fBlock / 28) * 100));
}
 
 
int PrintGameover(int _i, int _s)
{
    iCell = 0;
    gotoXY(31, 3); printf("%d   ", iCell);
    //while (getchar() != '\n'); 버퍼지우기 디버깅 필요
    gameoversound(_s);
    PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
    gotoXY(POPUPSTART_POSX + 11, POPUPSTART_POSY - 1);
    printf("Game Over!");
    gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1);
    printf("▶다  시  시  작");
    gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 3);
    printf("  랭          킹");
    gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 5);
    printf("  제          작");
    gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 7);
    printf("  게  임  종  료");
    while (_i)
    {
        if (GetAsyncKeyState(VK_UP))
        {
            menusound(_s);
            --iGameover;
        }
        if (GetAsyncKeyState(VK_DOWN))
        {
            menusound(_s);
            ++iGameover;
        }
        if (iGameover < 0) iGameover = 3;
        if (iGameover > 3) iGameover = 0;
        switch (iGameover)
        {
        case 0:    PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
 
            gotoXY(POPUPSTART_POSX + 11, POPUPSTART_POSY - 1);
            printf("Game Over!");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1);
            printf("▶다  시  시  작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 3);
            printf("  랭          킹");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 5);
            printf("  제          작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 7);
            printf("  게  임  종  료"); gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
            break;
        case 1: PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
            gotoXY(POPUPSTART_POSX + 11, POPUPSTART_POSY - 1);
            printf("Game Over!");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1);
            printf("  다  시  시  작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 3);
            printf("▶랭          킹");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 5);
            printf("  제          작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 7);
            printf("  게  임  종  료"); gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause"); break;
        case 2:PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
            gotoXY(POPUPSTART_POSX + 11, POPUPSTART_POSY - 1);
            printf("Game Over!");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1);
            printf("  다  시  시  작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 3);
            printf("  랭          킹");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 5);
            printf("▶제          작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 7);
            printf("  게  임  종  료"); gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause"); break;
        case 3: PopupLength(8, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
            gotoXY(POPUPSTART_POSX + 11, POPUPSTART_POSY - 1);
            printf("Game Over!");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1);
            printf("  다  시  시  작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 3);
            printf("  랭          킹");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 5);
            printf("  제          작");
            gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 7);
            printf("▶게  임  종  료"); gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause"); break;
        }
        if (GetAsyncKeyState(VK_RETURN))
        {
            switch (iGameover)
            {
            case 0:
                // 전역변수 초기화
                iTapSelect = 0, iDir = 0, iLevel = 1, iCell = 2, iProtein = 0, iCellUseUp = 0;
                fBlock = 0, fPrevExpLimits = 0, fCurExpLimits = 0, fElapsedExp = 0, fExtraElapesExp = 0, fLeftExp = 0, fTotalExp = 0;
                iExpFulling = 0, iFishNear1 = 0, iFishNear2 = 0, iGameover = 0;
                main(); break;
            case 1:break;
            case 2: _i = 0; system("cls"); PopupLength(15, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY-5);
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 1-5); printf("▣게임 제작");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 2 - 5); printf("-김");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 3 - 5); printf("프로젝트 디자인,");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 4 - 5); printf("플레이 화면 구성/디버깅");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 6 - 5); printf("-조");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 7 - 5); printf("사운드적용");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 8 - 5); printf("플레이화면 디버깅");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 10 - 5); printf("-이");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 11 - 5); printf("플레이 화면 디버깅");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 13 - 5); printf("-최");
                gotoXY(POPUPSTART_POSX + 2, POPUPSTART_POSY + 14 - 5); printf("타이틀 화면 구성/디버깅");
                gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");break;
            case 3:  gameexitsound(_s); system("cls");
                PopupLength(2, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
                gotoXY(POPUPSTART_POSX + 7, POPUPSTART_POSY + 1); printf("게임을 종료합니다.");
                gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25);
                Sleep(1500); exit(0);
                break;
            }
        }
    }
    return _i;
}
 
void CountDown()
{
    gotoXY(35, PLARY_POSY); printf("  3  "); Sleep(1000);
    gotoXY(35, PLARY_POSY); printf("  2  "); Sleep(1000);
    gotoXY(35, PLARY_POSY); printf("  1  "); Sleep(500);
    gotoXY(35, PLARY_POSY); printf("STRAT!"); Sleep(500);
    gotoXY(34, PLARY_POSY); printf("        ");
}
 
int PrintSoundOptions(int _s)
{
    int i = 0, j = 0, k = 0;
    if (_s = 3) { k = 1; j = 1; };   // 배경음 on 효과음 on
    if (_s = 2) { k = 1;  j = 0; };  // 배경음 on 효과음 off
    if (_s = 1) { k = 0; j = 1; };   // 배경음 off 효과음 on
    if (_s = 0) { k = 0; j = 0; };   // 배경음 off 효과음 off
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    SetConsoleTextAttribute(hConsole, RESET_COLOR);
    PopupLength(10, POPUP_WIDTH, POPUPSTART_POSX, POPUPSTART_POSY);
    gotoXY(POPUPSTART_POSX + 10, POPUPSTART_POSY + 1);
    printf("Sound Option");
    gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 4);
    printf("◁    효과음 켜기    ▶");
    gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 6);
    printf("◁    배경음 켜기    ▷");
    gotoXY(POPUPSTART_POSX + 3, POPUPSTART_POSY + 9);
    printf("저장 및 타이틀 : press ESC");
    while (1)
    {
        if (GetAsyncKeyState(VK_ESCAPE))
        {
            system("cls");
            break;
        }
        if (GetAsyncKeyState(VK_UP))--i;
        if (GetAsyncKeyState(VK_DOWN))    ++i;
 
        if (GetAsyncKeyState(VK_LEFT) && i == 0)--j;
        if (GetAsyncKeyState(VK_RIGHT) && i == 0)++j;
        if (GetAsyncKeyState(VK_LEFT) && i == 1)--k;
        if (GetAsyncKeyState(VK_RIGHT) && i == 1)++k;
 
        if (i > 1)i = 0;
        if (i < 0)i = 1;
        if (j > 1)j = 0; // 효과음
        if (j < 0)j = 1;
        if (k > 1)k = 0; // 배경음
        if (k < 0)k = 1;
 
        switch (i)
        {
        case 0:
            SetConsoleTextAttribute(hConsole, 240);
            if (j == 1)
            {
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 4);
                printf("◁    효과음 켜기    ▶");
                SetConsoleTextAttribute(hConsole, RESET_COLOR);
                gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 4);
                printf("◁    효과음 켜기    ▶"); break;
            }
            else if (j == 0)
            {
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 4);
                printf("◀    효과음 끄기    ▷");
                SetConsoleTextAttribute(hConsole, RESET_COLOR);
                gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 4);
                printf("◀    효과음 끄기    ▷"); break;
            }
        case 1:
            SetConsoleTextAttribute(hConsole, 240);
            if (k == 1)
            {
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 6);
                printf("◁    배경음 켜기    ▶");
                SetConsoleTextAttribute(hConsole, RESET_COLOR);
                gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 6);
                printf("◁    배경음 켜기    ▶"); break;
            }
            else if (k == 0)
            {
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 6);
                printf("◀    배경음 끄기    ▷");
                SetConsoleTextAttribute(hConsole, RESET_COLOR);
                gotoXY(POPUPSTART_POSX, POPUPSTART_POSY + 25); system("pause");
                gotoXY(POPUPSTART_POSX + 4, POPUPSTART_POSY + 6);
                printf("◀    배경음 끄기    ▷"); break;
            }
        }
        if (k == 1 && j == 1) _s = 3; // 배경음 on 효과음 on
        if (k == 1 && j == 0) _s = 2; // 배경음 on 효과음 off
        if (k == 0 && j == 1) _s = 1; // 배경음 off 효과음 on
        if (k == 0 && j == 0) _s = 0; // 배경음 off 효과음 off
    }
    return _s;
}
 
void menusound(int _s)   // 메뉴소리
{
    if (_s == 1 || _s == 3)    PlaySound(TEXT(SOUND_MENU_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void storesound(int _s)   // 상점 bgm
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_STORE_NAME), NULL, SND_FILENAME | SND_ASYNC | SND_LOOP);
}
void singlesound(int _s) // 단일공격 소리
{
    if (_s == 1 || _s == 3)    PlaySound(TEXT(SOUND_SINGLE_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void continuesound(int _s) // 연속공격 소리
{
    if (_s == 1 || _s == 3)    PlaySound(TEXT(SOUND_CONTINUE_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void wholesound(int _s)// 전체스킬 소리
{
    if (_s == 1 || _s == 3)    PlaySound(TEXT(SOUND_WHOLE_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void titlesound(int _s)   // 타이틀 bgm
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_TITLE_NAME), NULL, SND_FILENAME | SND_ASYNC | SND_LOOP);
}
void gameexitsound(int _s) //게임종료 소리
{
    if (_s == 1 || _s == 3)    PlaySound(TEXT(SOUND_GAMEEXIT_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void gameoversound(int _s) //게임오버 소리
{
    if (_s == 1 || _s == 3)    PlaySound(TEXT(SOUND_GAMEOVER_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void storystartsound(int _s)   // 스토리 시작소리
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_STORYSTART_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void plaryappearsound(int _s)   // 플라리 출현 소리
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_PLARYAPPEAR_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void plaryspeaksound(int _s)   // 플라리 말할때 bgm
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_PLARYSPEAK_NAME), NULL, SND_FILENAME | SND_ASYNC | SND_LOOP);
}
void storyendsound(int _s)   // 스토리 종료소리
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_STORYEND_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void chapter2sound(int _s)   // 챕터 2
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_CHAPTER2_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}
void ownerappearsound(int _s)   // 주인등장
{
    if (_s == 2 || _s == 3)    PlaySound(TEXT(SOUND_OWNERAPPEAR_NAME), NULL, SND_FILENAME | SND_ASYNC | 1);
}

