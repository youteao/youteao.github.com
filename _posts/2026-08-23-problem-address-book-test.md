---
layout: post
title: "address book"
date:   2026-06-10 20:30:13 +0800
categories: Default
tags: test Test
comments: 1
---

# [Python] 객체지향(OOP)과 파일 입출력을 활용한 파이썬 주소록 프로그램 만들기

안녕하세요! 오늘은 파이썬의 **클래스(Class)**와 **파일 입출력(File I/O)** 개념을 종합적으로 활용해 볼 수 있는 **CUI 주소록 관리 프로그램**을 함께 만들어보겠습니다.

단순히 메모리상에서만 작동하는 프로그램이 아니라, `address.txt` 파일과 연동하여 데이터를 영구적으로 저장하고 불러오는 구조까지 구현해 볼 수 있어 객체지향 기초를 다지기에 아주 좋은 실습 주제입니다.

---

## 📌 1. 프로젝트 개요 및 주요 기능

이 프로그램은 콘솔 환경에서 실행되는 연락처 관리 프로그램입니다. 다음과 같은 핵심 기능을 제공합니다.

* **연락처 생성 및 관리**: 이름, 전화번호, 이메일, 주소를 하나의 객체로 묶어 관리합니다.
* **데이터 영구 저장**: 파일 입출력을 통해 프로그램이 종료되어도 데이터가 유지됩니다.
* **선택형 인과 메뉴**: 1~4번 숫자를 입력하여 원하는 작업을 수행할 수 있습니다.

---

## 🔍 2. 프로그램 구조 분석

전체 코드의 구조를 한눈에 파악할 수 있도록 클래스 및 각 함수별 역할을 정리했습니다.

| 구분 | 이름 | 주요 역할 및 설명 |
| :--- | :--- | :--- |
| **클래스** | `Contact` | 연락처 정보(이름, 번호, 이메일, 주소)를 하나로 묶어주는 데이터 구조 |
| **함수** | `set_contact()` | 사용자로부터 키보드 입력을 받아 `Contact` 객체를 생성 |
| **함수** | `print_contact()` | 현재 등록된 모든 연락처 목록을 화면에 출력 |
| **함수** | `delete_contact()` | 입력받은 이름과 일치하는 연락처 정보를 리스트에서 삭제 |
| **함수** | `load_contact()` | `address.txt` 파일에서 저장된 데이터를 읽어와 리스트로 복원 |
| **함수** | `store_contact()` | 리스트에 있는 모든 연락처 데이터를 `address.txt` 파일에 저장 |
| **함수** | `print_menu()` | 사용자에게 메뉴를 보여주고 원하는 메뉴 번호를 입력받음 |
| **함수** | `run()` | 프로그램의 메인 루프를 제어하고 함수들을 연결 |

---

## 💻 3. 전체 소스 코드

전체 코드 내용은 아래와 같습니다.

> ```python
> class Contact:
>     def __init__(self, name, phone_number, e_mail, addr): #초기 주소 입력
>         self.name = name 
>         self.phone_number = phone_number
>         self.e_mail = e_mail
>         self.addr = addr
> 
>     def print_info(self):
>         print("이름: ", self.name) #이름 출력
>         print("폰번호: ", self.phone_number) #번호 출력
>         print("이메일: ", self.e_mail)#이메일 출력
>         print("주소: ", self.addr)# 주소 출력
> 
> def set_contact():
>     name = input("이름: ")#이름 입력
>     phone_number = input("폰번호: ")#폰번호 입력
>     e_mail = input("이메일: ")#이메일 입력
>     addr = input("주소: ")# 주소 입력
>     contact = Contact(name, phone_number, e_mail, addr)#contact 변수에 입력된 값들을 튜플로 저장
>     return contact #contact 번환
> 
> def print_contact(contact_list):
>     for contact in contact_list: # for반복문 contact_list의 값을 출력
>         contact.print_info() #contact의 값 출력
> 
> def delete_contact(contact_list, name): # 연락처 삭제
>     for i, contact in enumerate(contact_list): #contact_list의 인덱스 값과 변수를 함께 출력
>         if contact.name == name: #앞에서 입력한 값과 contact.name의 값이 같으면
>             del contact_list[i] #그 이름에 대한 정보 삭제
> 
> def load_contact(contact_list):
>     f = open("address.txt", "rt") #"address.txt"를 읽기 모드로 열기
>     lines = f.readlines() #각 요소를 리스트 형태로 저장
>     num = len(lines) / 4 #한 사람당 4줄의 정보를 가지기 때문에 4로 나누기
>     num = int(num) #range문에 넣을 수 있게 정수 형태로 변환
> 
>     for i in range(num): #저장된 사람의 수 만큼 반복
>         name = lines[4*i].rstrip('\n') # 줄바꿈을 없애고 name에 저장 이때 한 사람 당 4줄의 정보를 가지기 때문에 한사람 할때 마다 4줄 띄어 불러오기
>         phone = lines[4*i+1].rstrip('\n')# 줄바꿈을 없애고 phone에 저장
>         email = lines[4*i+2].rstrip('\n')# 줄바꿈을 없애고 email에 저장
>         addr = lines[4*i+3].rstrip('\n')# 줄바꿈을 없애고 addr에 저장
>         contact = Contact(name, phone, email, addr) #불러온 정보들을 list형태로 contact에 저장
>         contact_list.append(contact) #contact를 contact_list에 추가
>     f.close() #address.txt를 닫기
> 
> def store_contact(contact_list):
>     f = open("address.txt", "wt") #address.txt를 쓰기 모드로 열기
>     for contact in contact_list: #contact_list를 contact로 불러오기
>         f.write(contact.name + '\n') # address.txt에 이름 쓰기
>         f.write(contact.phone_number + '\n')# address.txt에 번호 쓰기
>         f.write(contact.e_mail + '\n')# address.txt에 이메일 쓰기
>         f.write(contact.addr + '\n')# address.txt에 주소 쓰기
>     f.close() #address.txt를 닫기
> 
> def print_menu(): # 사용자 인터페이스
>     print("1. 연락처 입력")
>     print("2. 연락처 출력")
>     print("3. 연락처 삭제")
>     print("4. 종료")
>     menu = input("메뉴선택: ") #사용할 매뉴 입력
>     return int(menu) #정수 형태로 입력된 값 반환
> 
> def run(): #모든 함수를 연결,작동해주는 함수
>     contact_list = [] #contact_list를 리스트로 생성
>     store_contact(contact_list) #load_contact함수 호출 -> store_contact함수 호출
>     while 1: #while 1 == while True
>         menu = print_menu() #사용자 인터페이스 열기
>         if menu == 1: #사용자가 입력한 값이 1이면
>             contact = set_contact() #set_contact 함수를 호출하여 contact에 저장
>             contact_list.append(contact) #contact_list contact를 추가
>         elif menu == 2:#사용자가 입력한 값이 2이면
>             print_contact(contact_list) #contact_list의 값을 출력
>         elif menu == 3:#사용자가 입력한 값이 3이면
>             name = input("Name: ") #지울 대상의 이름을 입력
>             delete_contact(contact_list, name) #입력한 값을 앞서 만든 contact_list와 입력한 값을 delete_contact에 넣어 호출
>         elif menu == 4:#사용자가 입력한 값이 4이면
>             store_contact(contact_list) #address.txt를 닫기
>             break #반복문 탈출
> 
> if __name__ == "__main__":
>     run()
> ```

---

## 🖥️ 4. 실행 예시 (Output)

실제 터미널에서 프로그램을 실행하면 다음과 같이 상호작용합니다.

```text
1. 연락처 입력
2. 연락처 출력
3. 연락처 삭제
4. 종료
메뉴선택: 1
이름: 홍길동
폰번호: 010-1234-5678
이메일: hong@email.com
주소: 서울시 강남구

1. 연락처 입력
2. 연락처 출력
3. 연락처 삭제
4. 종료
메뉴선택: 2
이름:  홍길동
폰번호:  010-1234-5678
이메일:  hong@email.com
주소:  서울시 강남구
```

---

## 💡 5. 코드 리뷰 및 발전 방향

기본적인 기능이 잘 구현되어 있지만, 실무 관점에서 다음과 같은 **개선점**들을 고민해 볼 수 있습니다.

1. **시작 시 파일 읽기 함수 호출 오류**
   * `run()` 함수 시작 지점에서 `load_contact(contact_list)` 대신 `store_contact(contact_list)`가 실행되고 있습니다. 이로 인해 프로그램 시작 시 기존에 저장되어 있던 `address.txt` 내용이 빈 데이터로 덮어씌워지는 문제가 발생합니다. `load_contact`로 수정이 필요합니다.
2. **`with` 구문을 활용한 안전한 파일 자원 관리**
   * `open()`과 `close()`를 명시적으로 작성하는 것보다, 파이썬의 `with open(...) as f:` 구문을 사용하면 파일 작업 중 에러가 발생하더라도 파일을 안전하게 닫아줄 수 있습니다.
3. **데이터 포맷의 표준화 (`JSON` 또는 `CSV`)**
   * 현재는 4줄 단위의 순수한 텍스트 형태로 데이터를 저장하고 있습니다. 데이터 간 경계가 모호해지거나 형식이 깨지는 것을 방지하기 위해 `json` 모듈이나 `csv` 포맷을 사용하면 훨씬 안정적인 데이터 처리가 가능해집니다.

---

오늘 작성한 파이썬 주소록 예제를 통해 클래스의 구조화 능력과 파일 입출력의 기초 흐름을 확실히 이해하셨기를 바랍니다!
