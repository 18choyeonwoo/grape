# 2_Trojan — subprocess 리버스 쉘 실습

GRAPE 보안 스터디 교육 자료 (Quokka RAT, author: 전재호/agamtt) 로 실습 진행함.
Docker 컨테이너 2개(hacker / victim) 격리 환경에서 리버스 쉘의 동작 원리를 학습하는 교육용 코드.

## 1단계 — 소켓 통신 (채팅)
- `listener.py` : hacker(C2) 쪽. 포트를 열고 연결을 기다린 뒤 메시지를 주고받음.
- `client.py` : victim 쪽. hacker에게 먼저 outbound 연결(reverse).

## 2단계 — subprocess 연결 (명령 실행)
- `c2_listener.py` : hacker가 명령어를 입력해서 전송.
- `payload.py` : victim 쪽에서 받은 명령을 subprocess로 실행하고 결과를 회신.

## 실행 순서
1. hacker 컨테이너에서 listener 먼저 실행 (`python3 c2_listener.py`)
2. victim 컨테이너에서 payload 실행 (`python3 payload.py`)

> IP `172.17.0.3` 은 Docker 컨테이너 환경값이라 본인 환경에 맞게 바꿔야 함.
> 격리된 실습 환경 외부에서 사용하지 말 것.
