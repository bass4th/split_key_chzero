# CHZero 왼쪽 ZMK 테스트 펌웨어

nice!nano v2 호환 nRF52840 클론, 왼쪽 29키 USB 단독 테스트 설정입니다.
ZMK v0.3.0에 고정했습니다. 오른쪽 무선 분할 및 OLED는 아직 설정하지 않았습니다.

## 배선

사용자 배선도를 **뒷면**으로 해석했습니다. 핀 표기는 MCU 인쇄 기준입니다.

- 행 위→아래: 024, 100, 011, 104, 106
- 본체 열 그림 왼쪽→오른쪽: 009, 113, 111, 010, 029, 002
- 단독 파란 키 열: 031
- 엄지키: R4/C0~C3, 파란 키: R3/C6
- 검은 띠가 행 공통선 방향: col2row
- 100은 P1.00, 113은 P1.13처럼 해석합니다.

위 연결은 그림 판독 결과이며 실물 입력 시험으로 확인해야 합니다.
앞면 순서로 변환하기 위해 본체 열과 엄지키 순서를 반전했습니다.

## 앞면 키 배열

```text
ESC   1  2  3  4  5
TAB   Q  W  E  R  T
CTRL  A  S  D  F  G
SHIFT Z  X  C  V  B
      GUI ALT SPACE BSPC
파란 키: ENTER
```

## 빌드와 설치

1. 이 파일들을 GitHub 저장소에 push합니다.
2. Actions의 `Build left firmware` 실행이 성공하면 `firmware` 아티팩트를 내려받아 압축을 풉니다.
3. 왼쪽 MCU를 데이터 USB 케이블로 연결합니다.
4. 보드의 부트로더 방식에 따라 리셋합니다. 일반적인 nice!nano 호환 UF2 부트로더는 RST와 GND를 짧게 두 번 연결하면 USB 드라이브가 나타납니다.
5. 빌드된 왼쪽 `.uf2` 파일을 해당 드라이브에 복사합니다.
6. 텍스트 편집기에서 각 키를 한 번씩 눌러 배열을 확인합니다.

GitHub Actions 빌드 성공: https://github.com/bass4th/split_key_chzero/actions/runs/42360634814

생성 파일: `firmware/left/chzero_left-nice_nano_v2-zmk.uf2` (로컬 다운로드). UF2 블록 형식을 검사했습니다. 실제 하드웨어 입력 확인은 남아 있습니다.
키가 반대로 나오면 matrix transform 순서를, 특정 행/열 전체가 작동하지 않으면 해당 GPIO 배정을 확인합니다.
OLED의 SDA/SCL과 컨트롤러 모델은 확인 후 추가합니다.

공식 문서: https://zmk.dev/docs/hardware-integration/new-shield
