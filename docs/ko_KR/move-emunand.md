# EmuNAND기반 데이터 이동

## 중요

이 페이지는 이전 EmuNAND의 데이터를 새로운 CFW SysNAND로 옮기고 이전 EmuNAND 파티션을 제거하는 방법을 안내하는 부가 섹션입니다. EmuNAND와 RedNAND는 [동일한 개념](http://3dbrew.org/wiki/NAND_Redirection)을 다른 방식으로 구현한 것입니다.

만약 여러분의 SD 카드의 `/luma/payloads/` 폴더에 `GodMode9.firm` 외의 페이로드 파일이 있다면, (Start)를 누르면서 부팅할 시에 화면에 표시되는 "chainloader menu" 에서 십자 패드와 (A) 버튼으로 조작하여 "GodMode9"을 선택하여야 합니다.

::: danger

이것은 Luma3DS 및 boot9strap가 이미 설치되어 있어야 가능합니다.

:::

## 준비물

- 설치된 EmuNAND
- 최신 버전의 [GodMode9](https://github.com/d0k3/GodMode9/releases/latest) (GodMode9 `.zip` 파일)

## 진행 방법

### 섹션 I - 준비 작업

1. 콘솔의 전원을 꺼 주세요
2. SD 카드를 컴퓨터에 삽입해 주세요
3. SD 카드의 `/luma/payloads/`폴더에 GodMode9 `.zip`안에 압축되있는 `GodMode9.firm`을 복사해 주세요
4. SD 카드의 루트로 GodMode9 `.zip`안에 압축이 되있는 `gm9` 폴더를 복사해 주세요
5. SD 카드를 콘솔에 다시 삽입해 주세요

### 섹션 II - SysNAND DSiWare 저장 데이터 백업

::: info

DSiWare 게임이나 저장 데이터에 대해 신경 쓰지 않는다연 이 섹션을 건너뛰어 주세요.

:::

1. (Start) 를 길게 누르고, 이 상태에서 콘솔의 전원을 켜 주세요. GodMode9이 실행될 겁니다
2. 만약 "Essential files backup not found" 메세지가 표시되면, (A) 룰 눌러서 백업을 만들고, 끝나면 (A) 를 눌러서 진행해 주세요
3. 만약 "RTC date&time seems to be wrong" 메세지가 표시되면 (A) 버튼을 눌러 하고, 날짜와 시간을 고친 다음 (A) 버튼을 눌러 계속해 주세요
    - 만약 RTC 날짜와 시간을 수정해야 했다면, 이 가이드 끝나고 본체 설정에서도 시간을 수정해야 합니다
4. `[2:] SYSNAND TWLN` -> `title`로 이동해 주세요
5. `00030004` 폴더에 (R) 을 누른 채 (A) 를 눌러 선택하고 "Copy to 0:/gm9/out"을 선택해 주세요
    - 이 과정은 콘솔에 DSiWare 게임이 많다면 시간이 좀 걸릴 수 있습니다
6. (B)를 두 번 눌러 메인 메뉴로 돌아가 주세요

### 섹션 III - GBA VC 저장 데이터 백업

::: info

GBA VC 게임이나 저장 데이터에 대해 신경 쓰지 않는다면 이 섹션을 건너뛰어 주세요.

:::

::: info

다른 종류의 버추얼 콘솔 게임(GBC, FC, 기타)에서 이 과정은 불필요합니다.

:::

::: info

게임은 `<TitleID>.gbavc.sav`의 이름으로 SD카드의 `/gm9/out/`폴더에 산출될 것입니다.

:::

::: info

`<TitleID>.gbavc.sav` 파일이 어떤 게임인지 구분하기 위해 (Home)을 눌러 액션 메뉴로 이동해 `Title Manager` -> [A:] SD CARD\`를 선택해 콘솔에 있는 모든 게임의 Title ID를 볼 수 있습니다.

:::

1. 과정대로 진행해 백업하고자 하는 GBA VC 게임 저장 데이터를 저장해 주세요:
    - GBA VC 게임을 실행해 주세요
    - GBA VC 게임을 종료해 주세요
    - (Start)를 누른 채 콘솔의 전원을 켜 Luma3DS chainloader 메뉴를 실행해 주세요
    - (A)를 눌러 GodMode9을 실행해 주세요
    - `[S:] SYSNAND VIRTUAL` 폴더로 이동해 주세요
    - `agbsave.bin`에서 (A)를 눌러 선택해 주세요
    - "AGBSAVE options..."를 선택해 주세요
    - "Dump GBA VC save"를 선택해 주세요
    - (A)를 눌러 진행해 주세요
    - (Start)를 눌러 콘솔을 다시 시작해 주세요

### 섹션 IV - EmuNAND를 SysNAND로 복사

1. (Start) 를 길게 누르고, 이 상태에서 콘솔의 전원을 켜 주세요. GodMode9이 실행될 겁니다
2. `[E:] EMUNAND VIRTUAL` 로 이동해 주세요
3. `nand.bin`에 (A)를 눌러 선택하고 "NAND image options..."를 선택하고 "Restore SysNAND (safe)"를 선택해 주세요
4. (A)를 눌려 SysNAND 쓰기 잠금을 풀고 주어진 키 조합을 입력해 주세요
    - 이 과정은 boot9strap를 덮어쓰지 않습니다
5. SysNAND (lvl1) 쓰기 잠금을 풀기 위해 주어진 키 조합을 입력해 주세요
    - 이 과정은 시간이 좀 걸릴 것입니다
6. 작업이 완료되면 (A)를 눌러서 계속해 주세요
7. 만약 메세지가 표시되면, (B) 를 눌러서 쓰기잠금을 거부해 주세요
8. (B)를 눌러 메인 메뉴로 돌아가 주세요

### 섹션 V - DSiWare 저장 데이터 파일 복원

::: info

이전에 DSiWare 저장 데이터를 백업하지 않았다면 이 섹션을 건너뛰어 주세요.

:::

1. `[0:] SDCARD` -> `gm9` -> `out`으로 이동해 주세요
2. `00030004` 폴더에 (Y)를 눌러 복사해 주세요
3. (B)를 두 번 눌러 메인 메뉴로 돌아가 주세요
4. `[2:] SYSNAND TWLN` -> `title`로 이동해 주세요
5. (Y)를 눌러 `00030004` 폴더를 붙여넣어 주세요
6. "Copy path(s)"를 선택해 주세요
7. (A)를 눌려 SysNAND (lvl1) 쓰기 잠금을 풀고 주어진 키 조합을 입력해 주세요
8. "Overwrite file(s)"를 선택해 주세요
    - 이 과정은 콘솔에 DSiWare 게임이 많다면 시간이 좀 걸릴 수 있습니다
9. 만약 메세지가 표시되면, (B) 를 눌러서 쓰기잠금을 거부해 주세요
10. (B)를 두 번 눌러 메인 메뉴로 돌아가 주세요

### 섹션 VI - GBA VC 저장 데이터 파일 복원

::: info

이전에 GBA VC 저장 데이터를 백업하지 않았다면 이 섹션을 건너뛰어 주세요.

:::

::: info

`<TitleID>.gbavc.sav` 파일이 어떤 게임인지 구분하기 위해 (Home)을 눌러 액션 메뉴로 이동해 `Title Manager` -> [A:] SD CARD\`를 선택해 콘솔에 있는 모든 게임의 Title ID를 볼 수 있습니다.

:::

1. (R)을 누른 채 (Start)를 눌러 콘솔의 전원을 꺼 주세요
2. 콘솔을 SysNAND 상태로 시작해 주세요
3. 과정대로 진행해 모든 GBA VC 게임 저장 데이터를 백업해 주세요
    - GBA VC 게임을 실행해 주세요
    - GBA VC 게임을 종료해 주세요
    - (Start)를 누른 채 콘솔의 전원을 켜 Luma3DS chainloader 메뉴를 실행해 주세요
    - (A)를 눌러 GodMode9을 실행해 주세요
    - `[0:] SDCARD` -> `gm9`으로 이동해 주세요
    - 복구하길 희망하는 `<TitleID>.gbavc.sav`에서 (Y)를 눌러 복사해 주세요
    - (B)를 눌러 메인 메뉴로 돌아가 주세요
    - `[S:] SYSNAND VIRTUAL` 폴더로 이동해 주세요
    - `agbsave.bin`에서 (A)를 눌러 선택해 주세요
    - "AGBSAVE options..."를 선택해 주세요
    - "Inject GBA VC save"를 선택해 주세요
    - (A)를 눌러 진행해 주세요
    - (Start)를 눌러 콘솔을 다시 시작해 주세요
    - GBA VC 게임을 실행해 주세요
    - GBA VC 게임을 종료해 주세요

### 섹션 VII - SysNAND 백업

1. (Start) 를 길게 누르고, 이 상태에서 콘솔의 전원을 켜 주세요. GodMode9이 실행될 겁니다

<!--@include: ./_include/nand-backup.md -->

1. **SD 카드의 모든 파일을 컴퓨터에 백업해두세요. 다음 단계에서 SD 카드의 모든 파일이 삭제됩니다.**

### 섹션 VIII - SD 카드 포맷

1. (Start) 를 길게 누르고, 이 상태에서 콘솔의 전원을 켜 주세요. GodMode9이 실행될 겁니다

<!--@include: ./_include/format-sd-gm9.md -->

1. (R) 버튼과 (B)를 동시에 눌러 SD 카드를 뺄 준비를 해 주세요
2. SD 카드를 컴퓨터에 삽입해 주세요
3. SD 카드의 모든 파일을 도로 복사해 주세요
    - SD 카드에 있는 `boot.firm`을 백업한 파일로 교체했는지 확인해 주세요
4. SD 카드를 콘솔에 다시 삽입해 주세요
5. (A)를 눌러 SD 카드를 다시 마운트해 주세요
6. (Start)를 눌러 콘솔을 다시 시작해 주세요

___

::: tip

[마무리 단계](finalizing-setup) 로 돌아갑니다

:::
