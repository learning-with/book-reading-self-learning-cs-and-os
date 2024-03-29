# 파일 시스템
## 파일과 디렉터리
### 파일file
하드 디스크나 SSD와 같은 보조기억장치에 저장된 관련 정보의 집합

의미 있고 관련 있는 정보를 모은 논리적 단위

모든 파일에는 이름과 파일을 실행하기 위한 정보, 파일 관련 부가 정보인 속성attribute 또는 메타데이터metadata를 가짐

#### 파일 속성과 유형
|속성 이름|의미|
|:--:|:--:|
|유형|운영체제가 인지하는 파일의 종류를 나타낸다|
|크기|파일의 현재 크기와 허용 가능한 최대 크기를 나타낸다|
|보호|어떤 사용자가 해당 파일을 읽고, 쓰고, 실행할 수 있는지를 나타낸다|
|생성 날짜|파일이 생성된 날짜를 나타낸다|
|마지막 접근 날짜|파일에 마지막으로 접근한 날짜를 나타낸다|
|마지막 수정 날짜|파일이 마지막으로 수정된 날짜를 나타낸다|
|생성자|파일을 생성한 사용자를 나타낸다|
|소유자|파일을 소유한 사용자를 나타낸다|
|위치|파일의 보조기억장치 상의 현재 위치를 나타낸다|

파일유형은 운영체제가 인식하는 파일 종류이므로 확장자를 이용해 파일 유형을 알림
|파일 유형|대표적인 확장자|
|:--:|:--:|
|실행파일|없는 경우, exe, com, bin|
|목적 파일|obj, o|
|소스 코드 파일|c, cpp, cc, java, asm, py|
|워드 프로세서 파일|xml, rtf, doc, docx|
|라이브러리 파일|lib, a, so, dll|
|멀티미디어 파일|mpeg, mov, mp3, pm4, avi|
|백업/ 보관 파일|rar, zip, tar|

#### 파일 연산을 위한 시스템 호출
응용 프로그램은 파일을 다루기 위해서 운영체제에 시스템 호출

### 디렉터리
이전에는 1단계 디렉터리single-level directory였으나, 컴퓨터 용량이 커지면서 트리 구조 디렉터리tree-structured directory로 여러 계층으로 관리

#### 절대 경로와 상대경로
절대경로absolute path: 루트 디렉터리에서 자기 자신까지 이르는 고유한경로

상대 경로relative path: 현재 디렉터리부터 시작하는 경로

#### 디렉터리 연산을 위한 시스템 호출
#### 디렉터리 엔트리
디렉터리는 보조기억장치에 테이블 형태의 정보로 저장됨

## 파일 시스템
파일과 디렉터리를 보조기억장치에 저장하고 접근할 수 있게 하는 운영체제 내부 프로그램

### 파티셔닝과 포매팅
#### 파티셔닝partitioning
저장 장치의 논리적인 영역을 구획하는 작업

파티셔닝 작업을 통해 나누어진 각 영역은 파티션partition

#### 포매팅formatting
파일 시스템을 설정하여 어떤 방식으로 파일을 저장하고 관리할 것인지를 결정하고, 새로운 데이터를 쓸 준비를 하는 작업

### 파일 할당 방법
#### 연속 할당contiguous allocation
보조기억장치 내 연속적인 블록에 파일을 할당하는 방식
- 외부 단편화를 야기함

#### 연결 할당linked allocation
각 블록 일부에 다음 블록의 주소를 저장하여 각 블록이 다음 블록을 가리키는 형태로 할당하는 방식
- 첫 번째 블록부터 하나씩 읽어야 함
- 하드웨어 고장이나 오류 발생 시 해당 블록 이후 블록은 접근할수 없음 
#### 색인 할당indexed allocation
파일의 모든 블록 주소를 색인 블록index block이라는 하나의 블록에 모아 관리하는 방식

### 파일 시스템 살펴보기
#### FAT 파일 시스템
각 블록에 포함된 다음 블록의 주소들을 한데 모아 파일 할당 테이블FAT, File Allocation Table에 관리

#### 유닉스 파일 시스템
i-node 색인 블록을 기반으로 파일의 데이터 블록들을 찾는 방식
- 블록 주소 중 열두 개에는직접 블록 주소를 저장
- 충분하지 않다면 열세 번째 주소에 단일 간접 블록 주소를 저장
- 충분하지 않다면 열네 번째 주소에 이중 간접 블록 주소를 저장
- 충분하지 않다면 열다섯 번째 주소에 삼중 간접 블록 주소를 저장
