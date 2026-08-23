---
layout: post
title:  "problems"
date:   2017-03-24 01:30:13 +0800
categories: default
tags: test syntax
---

주소록 실습
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
