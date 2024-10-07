### 1. открыть консоль и зайти по ssh на ВМ

![image](https://github.com/user-attachments/assets/3b9cdaf6-68ed-4814-bc5b-301c3e4e52e1)


### 2. открыть вторую консоль и также зайти по ssh на ту же ВМ (можно в докере 2 сеанса) & 3. запустить везде psql из под пользователя postgres

![image](https://github.com/user-attachments/assets/db4ad85d-8c35-4e2f-add2-eb14d6046aeb)


### 4. сделать в первой сессии новую таблицу и наполнить ее данными

![image](https://github.com/user-attachments/assets/6f2fdac2-035f-4a55-b97c-a25a63d8ace8)
![image](https://github.com/user-attachments/assets/04372c8e-8df6-4d66-bd5f-5a40265865c8)


### 5. посмотреть текущий уровень изоляции:

![image](https://github.com/user-attachments/assets/55e333cd-fc10-457a-810c-333fad16a792)


### 6. начать новую транзакцию в обеих сессиях с дефолтным (не меняя) уровнем

![image](https://github.com/user-attachments/assets/97772105-a28c-41d8-983b-535e2cf5d8a2)


### 7. в первой сессии добавить новую запись

![image](https://github.com/user-attachments/assets/3eeef639-7764-442a-817c-b0043af28441)


### 8. сделать запрос на выбор всех записей во второй сессии

![image](https://github.com/user-attachments/assets/27bebb58-2565-4457-9d0d-5af2767bd31b)


### 9. видите ли вы новую запись и если да то почему? 
Нет, запись не видно. Причина заключается в том, что транзакция находится на уровне read commited. Нам видно только зафиксированные данные, а т.к. первая транзакция ещё не завершена и данные не были закомичены, мы их не видим. Грязное чтение на этом уровне запрещено!


### 10. завершить транзакцию в первом окне

![image](https://github.com/user-attachments/assets/77828a48-56ec-4a0f-a5b4-a338cb68912a)


### 11. сделать запрос на выбор всех записей второй сессии

![image](https://github.com/user-attachments/assets/55c61717-045b-43ca-85c3-b12899268662)


### 12. видите ли вы новую запись и если да то почему?
Да, запись отображается. Данные были зафиксированы первой транзакцией и теперь все транзакции уровня read commited увидят новую запись.


### 13. завершите транзакцию во второй сессии

![image](https://github.com/user-attachments/assets/47e9c80d-a169-4fe9-9d4f-09758749f575)


### 14. начать новые транзакции, но уже на уровне repeatable read в ОБЕИХ сессиях

![image](https://github.com/user-attachments/assets/3e1650c0-bb27-4de6-9265-ada6110bdbe7)


### 15. в первой сессии добавить новую запись

![image](https://github.com/user-attachments/assets/5ca91126-5e5b-4c5e-8b3e-63a323d54d6c)


### 16. сделать запрос на выбор всех записей во второй сессии

![image](https://github.com/user-attachments/assets/45179df0-7a97-4338-a1fe-64d3c15bb1bf)



### 17. видите ли вы новую запись и если да то почему?
Нет, не видно. Repeatable read более строгий уровень изоляции. На нём тоже запрещено грязное чтение!


### 18. завершить транзакцию в первом окне

![image](https://github.com/user-attachments/assets/3fed7a73-60f2-49f1-af7d-c6cd2c1815b5)


### 19. сделать запрос во выбор всех записей второй сессии

![image](https://github.com/user-attachments/assets/297a1061-0259-468a-8102-46eca47a0845)


### 20. видите ли вы новую запись и если да то почему?
Нет. На уровне repeatable read видны только те записи, которые были закомичены к моменту начала транзацкии.

