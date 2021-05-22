# TonalityAnalysis
#Аналіз тональності текстів за допомогою згорткової нейронної мережі

![gif](/docs/tonal.gif)
# Налаштування проекту
Для початку потрібно:
1.  Встановити середовище виконання [Python](https://www.python.org/ftp/python/3.9.4/python-3.9.4-amd64.exe)

2. Клонувати проект за допомогою команди `git clone https://github.com/AndrewDmytryshyn/TonalityAnalysis.git`

3. Встановити всі потрібні залежності командою `pip install -r requirements.txt`

>Документація знаходиться [тут](./docs/readme.md)
## Usage

### Simple Training
Для початку потрібно:
* Підготувати 3 датасети (були викоритані такі [датасети](http://study.mokoron.com/))
    * 1 датасет з текстами негативного змісту
    * 1 датасет з текстами позитивного змісту
    * 1 нерозмічений дата сет
    
*  Натренерувати Word2Vec-модель
    * завантажити нерозмічений датасет у директорію src/data
    * у модулі word2vec_trainer вказати к-ть оброблювальної інформації
    * запустити word2vec_trainer та дочекатися завершення
    * у директорії src/w2v з'явиться навчена модель
    
*  Натренерувати згорткову нейронну мережу
    * завантажити розмічені датасети у директорію src/data
    * у модулі cnn_trainer налаштувати мережу
    * запустити cnn_trainer та дочекатися завершення
    * у директорії src/cnn з'явиться навчена модель
    * декілька раз натренерувати модель для покращення результатів
    
### Analise
* Подати в модуль tonality текст для аналізу
* Отримаємо відповідь у форматі настрій
## Example
![example](/docs/example.jpg)
## Учасники
* [Андрій Дмитришин](https://github.com/AndrewDmytryshyn)
* [Віталій Чередник](https://github.com/vitaliycherednik)
