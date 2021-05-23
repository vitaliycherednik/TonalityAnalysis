# Згорткова нейронна мережа


## Вступ
Згорткова нейронна мережа, СНС, CNN – основний інструмент для класифікації та розпізнавання об'єктів, облич на фотографіях, розпізнавання мови. Є безліч варіантів застосування CNN, такі як Deep Convolutional Neural Network (DCNN), Region-CNN (R-CNN), Fully Convolutional Neural Networks (FCNN), Mask R-CNN та інші.

"Згортка" – універсальна операція. Її можна застосувати для будь-якого сигналу, чи то дані з датчиків, чи аудіосигнал, чи картинка.
Згорткові нейронні мережі добре застосовуються там, де потрібно побачити шматочок або всю послідовність цілком і зробити якийсь висновок з цього. Тобто це завдання, наприклад, детекції спаму, аналізу тональності або вилучення іменованих сутностей. Однак у згортальних нейронних мереж є істотний недолік - вони можуть працювати тільки зі входом фіксованого розміру (тому що розміри матриць в мережі не можуть змінюватися в процесі роботи). 

Інша важлива особливість CNN в комп'ютерному зорі це можливість використання ваг мережі натренованої на одному великому датасеті (типовий приклад - ImageNet) в інших завданнях комп'ютерного зору. В NLP завданнях семантична близькість джерела на якому заздалегідь тренувалася мережа грає важливу роль, тобто мережа, натренована на рецензіях до фільмів, буде добре працювати на іншому датасеті з кінорецензій. До того ж, використання тих же embedding для слів збільшує успіх трансферу.

![embedding](/docs/embedding.png)
Ця картинка практично повністю пояснює, як ми працюємо з текстом за допомогою CNN.
## Архітектура
![CNN](/docs/CNN.png)

Вхідними даними CNN є матриця з фіксованою висотою n, де кожен рядок являє собою векторне відображення токена в просторі ознак розмірності k. Для формування простору ознак часто використовують інструменти дистрибутивної семантики, такі як Word2Vec, Glove, FastText і т.д.

На першому етапі вхідна матриця обробляється шарами згортки. Як правило, фільтри мають фіксовану ширину, рівну розмірності простору ознак, а для підбору розмірів у фільтрів налаштовується тільки один параметр - висота h. Виходить, що h - це висота суміжних рядків, що розглядаються фільтром спільно. Відповідно, розмірність вихідної матриці ознак для кожного фільтра варіюється в залежності від висоти цього фільтра h і висоти вихідної матриці n.

Далі карта ознак, отримана на виході кожного фільтра, обробляється шаром субдискретизації з певною функцією ущільнення (на зображенні - 1-max pooling), тобто зменшує розмірність сформованої карти ознак. Таким чином витягується найбільш важлива інформація для кожної згортки незалежно від її положення в тексті. Іншими словами, для використовуваного векторного відображення комбінація шарів згортки і шарів субдискретизації дозволяє витягувати з тексту найбільш значущі n-грами.

Після цього карти ознак, розраховані на виході кожного шару субдискретизації, об'єднуються в один загальний вектор ознак. Він подається на вхід прихованому повнозв'язному шару, а потім надходить на вихідний шар нейронної мережі, де і розраховуються підсумкові мітки класів.