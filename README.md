# DB1
Домашнее задание к занятию «Базы данных»



# Домашнее задание к занятию «Базы данных, их типы» - Мельник Юрий Александрович


## Задание 1

### СУБД
## Кейс

Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для каждой предметной области.

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему?

1. `Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.`
 
	1. `Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы?`
 
2. `Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для     CRM? СУБД должны быть    гибкими и быстрыми.`
	1. `Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?`

3. `Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.`
	1. `Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это реализовать?`
	
	
	
	
	

## Решение 1
1. ` `
 





## Задание 2
## Транзакции
2.1. `Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.`  

2.1*. `Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?`  
### Приведите ответ в свободной форме.

## Решение 2
2.1. `Пополнение счета в ручном режиме`  
 1.  Выбор счета для оплаты, сумма больше или равна сумме оплаты за услуги связи.  
 2. Подтверждаем перевод в сторону нашего оператора связи!получаем уведомление о списании средств!  
 3. Сумма перевода замораживается на счету абонента связи. Именно так и работает банковская система деньги в состоянии “HOLD”.  
 4. Инициализируеться перевод денежных средств на счет провайдера.  
 5. Ждем подтверждения от провайдера о зачисление средств.  
 6. Получаем подтверждение от провайдера, производим реальное списание средств.  
 7. При успешном прохождении платежа уведомление абонента о успешном проведении платежа. В случаи каких то ошибок производим отмену транзакции, возвращаем деньги на счет, уведомляем об ошибках при платеже  

2.1*. `Пополнение счета в автоматическом режиме`  
 1. В дату платежа, банк, проверяет есть ли необходимая сумма на указанном счете!  
 2. Банк инициализирует перевод на счет Телекоммуникационной компании, уведомляет абонента о списании денежных средств.  
 3. Банк ждет некоторое время получения подтверждения о зачислении платежа.  
 4. Подтверждение получено! банк производит реальное списание замороженных средств. уведомляет клиента о зачислении платежа. В случаи ошибок возвращаем замороженную сумму на счет клиента, уведомляем об ошибках при проведении платежа.  



## Задание 3.
## SQL vs NoSQL

3.1. `Напишите пять преимуществ SQL-систем по отношению к NoSQL.`  

3.1.* `Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.`  

### Приведите ответ в свободной форме.

3.1. `Преимущества SQL-систем по отношению к NoSQL.`  
 1. `В SQL-базах данных используется транзакционная модель, которая позволяет сохранять целостность данных и обеспечивать ACID`  
 2. `Схема данных: SQL-база данных имеет строгую схему данных, которая определяет типы данных и связи между таблицами.`  
 3. `Гибкость запросов: SQL имеет очень мощный язык запросов, что делает его лучшим выбором для сложных запросов, связанных с большим количеством таблиц.`  
 4. `SQL-базы данных универсальны, предназначены для решения широкого круга задач`  
 5. `Надежность, высокая производительность, предназначены для обработки больших данных и транзакций`  
 6. `Простота в использовании и обслуживании`  
 7. `Поддержка крупных поставщиков баз данных`  


3.1.* `Преимущества у NewSQL систем перед SQL и NoSQL.`  
    Современные БД можно поделить на два больших класса SQL и NoSQL. Каждый из этих классов обладает своими преимуществами и недостатками.  
   
    SQL БД поддерживают транзакции  ACID , мощный язык запросов SQL! Но имеют много накладных расходов связанных с обработкой транзакций, многопоточности.   
    Данные расходы начинают быстро препятствовать нормальной работоспособности при больших объемах обрабатываемых данных.   
    Nosql системы не имеют ограничений реляционных БД, но плохо подходят для хранения каких то структурированных данных, плохо поддерживают ACID.   
    Преодолеть перечисленные трудности призваны NewSQL БД. NewSQL объеденили в себе основные преимущества современных SQL и БД NoSQL . как таковые  NewSQL БД по поддерживают флэш-память/SSD программно или на аппаратном уровне. Появление систем NewSQL это ответ на требование времени - обработку больших объемов данных с поддержкой ACID. Разработчики систем  NewSQL утверждают, что системы приблизительно в 50 раз быстрее, чем традиционный OLTP RDBMS (реляционных транзакционных систем). Это существенный прирост производительности!   







