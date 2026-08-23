---
layout: post
title:  "problems"
date:   2017-03-24 01:30:13 +0800
categories: default
tags: test syntax
---

파일 입출력 
> ```python
> w = ''
> a = open("C:/Python/새파일.txt", 'w')
> while True:
>     b = input("이름을 입력하세요:")
>     c = input("점수을 입력하세요:")
>     w = w + (f"{b}:{c} ")
>     if input("계속하시겠습니까?(y/n):") == "n":
>         break
> a.write(w)
> a.close()
> a = open("C:/Python/새파일.txt", 'r')
> while True:
>     d = a.readline()
>     if not d: break
>     print(d)
> a.close()
> ```


클레스-연습
> ```python
> def square(a, b):
>     return (a+b)*2, a*b
> def curcle(a):
>     return a * 6.28, a*a*3.14
> 
> 
> while True:
>     a = input("1:사각형, 2:원 , 3:종료>>")
>     if a == '1':
>         b,c =square(int(input("첫번째 수를 입력하세요:")),int(input("두번째 수를 입력하세요:")))
>         print(f"사각형의 둘래는{b}, 넒이는{c} 입니다")
>     elif a == '2':
>         b,c = curcle(int(input("첫번째 수를 입력하세요:")))
>         print(f"사각형의 둘래는{b}, 넒이는{c} 입니다")
>     elif a == '3':
>         break
>     else:
>         print("잘못 입력하였습니다.")
> ```

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

클레스-창작
> ```python
> # 1. 총기 클래스
> class Weapon:
>     def __init__(self, name):
>         self.name = name
>         weapon_stats = {"SKS": 75, "SCAR-L": 42, "AWM": 100, "권총": 25}
>         self.damage = weapon_stats.get(name, 20)
> 
> 
> # 2. 투척류 클래스들 (기존)
> class Throwable:
>     def __init__(self, name):
>         self.name = name
> 
>     def use(self, target):
>         pass
> 
> 
> class Grenade(Throwable):
>     def __init__(self):
>         super().__init__("수류탄")
>         self.damage = 80
> 
>     def use(self, target):
>         print(f"💥 핀을 뽑고 수류탄을 던졌습니다! 쾅! (데미지: {self.damage})")
>         target.take_damage(self.damage)
> 
> 
> # 3. 🆕 회복 아이템 부모 클래스
> class HealItem:
>     def __init__(self, name, heal_amount):
>         self.name = name
>         self.heal_amount = heal_amount  # 회복량
> 
>     def use(self, player):
>         """자식 클래스에서 재정의할 회복 함수"""
>         pass
> 
> 
> # 4. 🆕 구급상자 클래스 (HealItem 상속)
> class FirstAidKit(HealItem):
>     def __init__(self):
>         super().__init__("구급상자", 75)  # 이름과 회복량(75) 전달
> 
>     def use(self, player):
>         print(f"🩹 [{player.nickname}]이(가) 구급상자를 사용하여 상처를 붕대로 감습니다... (체력 +{self.heal_amount})")
>         player.restore_health(self.heal_amount)
> 
> 
> # 5. 🆕 에너지 음료 클래스 (HealItem 상속)
> class EnergyDrink(HealItem):
>     def __init__(self):
>         super().__init__("에너지 음료", 25)  # 이름과 회복량(25) 전달
> 
>     def use(self, player):
>         print(f" energética 캔을 따서 마십니다! 🥤 [{player.nickname}] (체력 +{self.heal_amount})")
>         player.restore_health(self.heal_amount)
> 
> 
> # 6. 플레이어 클래스 (회복 아이템 기능 추가)
> class BattleGroundPlayer:
>     def __init__(self, nickname, weapon,throwable=None, heal_item=None):
>         self.nickname = nickname
>         self.weapon = weapon
>         self.throwable = throwable
>         self.heal_item = heal_item  # 🔗 회복 아이템 장착 슬롯 추가
>         self.health = 100
>         self.is_alive = True
> 
>     def shoot(self, target):
>         if not self.is_alive or not target.is_alive:
>             return
>         print(f"[{self.nickname}]이(가) [{target.nickname}]에게 {self.weapon.name} 사격! 🎯")
>         target.take_damage(self.weapon.damage)
> 
>     def throw_item(self, target):
>         if not self.is_alive or self.throwable is None:
>             return
>         print(f"[{self.nickname}]이(가) [{target.nickname}]쪽으로 {self.throwable.name} 투척!")
>         self.throwable.use(target)
> 
>     def use_heal_item(self):
>         """회복 아이템을 사용하는 함수"""
>         if not self.is_alive:
>             print(f"[{self.nickname}]은(는) 기절하여 회복할 수 없습니다.")
>             return
> 
>         if self.heal_item is None:
>             print(f"[{self.nickname}]은(는) 가진 회복 아이템이 없습니다!")
>             return
> 
>         print(f"[{self.nickname}]이(가) 가방에서 회복 아이템을 꺼냅니다.")
>         self.heal_item.use(self)  # 🔗 내 자신(self)을 전달해서 내 체력을 채우게 함!
> 
>     def restore_health(self, amount):
>         """체력을 회복하는 함수"""
>         self.health += amount
>         if self.health > 100:
>             self.health = 100  # 체력은 최대 100까지만 회복 가능
>         print(f"✨ [{self.nickname}] 체력 회복 완료! 현재 체력: {self.health}")
> 
>     def take_damage(self, amount):
>         self.health -= amount
>         if self.health <= 0:
>             self.health = 0
>             self.is_alive = False
>             print(f"💀 [{self.nickname}]이(가) 치명상을 입고 로비로 사출되었습니다.")
>         else:
>             print(f"🛡️ [{self.nickname}] 남은 체력: {self.health}")
> 
> 
> # --- 객체 생성 및 테스트 ---
> 
> kit = FirstAidKit()  # 구급상자 객체 생성 (회복량 75)
> Drink = EnergyDrink()
> grenade = Grenade()
> 
> # 플레이어가 M416과 구급상자를 가지고 시작 (현재 체력 50 상태)
> player1 = BattleGroundPlayer(nickname=input('닉네임 설정'),weapon=input("총 선택 :SKS: 75, SCAR-L: 42, AWM: 100, 권총: 25:"), heal_item=kit)
> player2 = BattleGroundPlayer(nickname=input('닉네임 설정'),weapon=input("총 선택 :SKS: 75, SCAR-L: 42, AWM: 100, 권총: 25:"), heal_item=kit)
> player1.shoot(player2)
> player2.throw_item(player1)
> player1.use_heal_item()
> player2.use_heal_item()
> player2.shoot(player1)
> player1.shoot(player2)
> ```
