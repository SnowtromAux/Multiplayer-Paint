# Проект: Frontend и Backend

Проектът е разделен на две части: **клиент** (frontend) и **сървър** (backend).  
Началната точка на проекта е: `/backend/app.js`.

---

## Сървър (Backend)

Сървърът използва сензитивни данни от `.env` файл за по-голяма сигурност.  
Използва рутери за навигация между страниците във фронтенда. Той отговаря за показването на страниците спрямо линка, изписан в браузъра.  
В момента са дефинирани три рутера:

1. `/` - Показва **Home Page** от фронтенда.
2. `/solo/:id` - Показва самостоятелна игра с уникален номер `id`.
3. `/party/:id` - Показва парти игра с код на парти `id`.

### Middleware
Сървърът използва три middleware-a:
1. `express.json` - Автоматично парсва JSON данни, изпратени в тялото на HTTP заявки.
2. `cors` - Позволява връзка на всички потребители в мрежата с приложението.
3. `express.static()` - Сервира статични файлове (HTML, CSS, JavaScript, изображения и други ресурси).

### Контролери
Сървърът работи с два основни контролера:

#### 1. `PartyControl`
Грижи се за събитията, свързани с партита:
- `socket.on("join-party", ...)` → Вкарва потребител в парти стая.
- `socket.on("leave-party", ...)` → Изкарва потребител от парти стая.
- `socket.on("create-party", ...)` → Създава парти и го записва в сървъра.
- `socket.on("delete-party", ...)` → Изтрива парти от сървъра.
- `socket.on("search-party", ...)` → Намира парти, взима данните му и ги връща на потребителя.
- `socket.on("update-party", ...)` → Обновява състоянието на парти и го изпраща към всички в стаята.
- `socket.on("start-game", ...)` → Уведомява участниците в стаята, че играта е стартирана.

#### 2. `GameControl`
Грижи се за събитията, свързани с играта:
- `socket.on("create-figure", ...)` → Изпраща съобщение за създаване на фигура.
- `socket.on("update-figure", ...)` → Изпраща съобщение за промяна на фигура (редакция, изтриване и др.).
- `socket.on("finish-figure", ...)` → Уведомява, че фигура е завършена.
- `socket.on("update-history", ...)` → Управлява историята на играта (напр. undo/redo).

---

## Клиент (Frontend)

Клиентската част съдържа четири основни папки:

1. **`assets`**  
   Съдържа всички снимки, икони и звуци, необходими за играта.

2. **`css`**  
   Съдържа стилизацията на всички страници на приложението.

3. **`js`**  
   Отговаря за логиката на играта.

4. **`views`**  
   Съдържа HTML страниците на приложението.

Документацията се фокусира основно върху папка `js`, където се намира логиката на приложението.

---

### Структура на `js`

#### 1. `commons`
Съдържа основните компоненти на приложението, разделени на четири файла:
- `constants.js` → Основни константи, използвани в цялото приложение.
- `functions.js` → Основни функции, използвани в цялото приложение.
- `storage.js` → SessionStorage за трансфер на несензитивни данни (напр. име на потребител).
- `variables.js` → Основни променливи на приложението.

#### 2. `menus`
Логика за взаимодействие на потребителя с различните страници:
- `game.js` → Логика за страницата на играта.
- `home.js` → Логика за началната страница.

#### 3. `objects`
Класове, които се използват в приложението:
- `Player.js` → Държи данни за потребителя (име, снимка, id, парти, игра и др.).
- `Party.js` → Управлява данни за парти (код, участници, текущ играч и др.), комуникирайки със сървъра чрез сокети.
- `Canvas.js` → Платно за рисуване, което съдържа данни като:
  - **Canvas** → HTML елемент за рисуване.
  - **Ctx** → Контекст за рисуване върху платното.
  - **Canvas_width/Canvas_height** → Размери на платното.
  - **Zoom** → Процент на мащабиране.
  - **Cur_figure** → Текущата фигура, която се рисува.
  - **Cur_canvas_data** → Пиксели на текущото платно.
  - **All_canvas_data** → Пиксели от историята на всички платна.
  - **Cur_canvas_index** → Текущ индекс в историята.
  - **Ивент слушатели** → Слушат за създаване, промяна и завършване на фигури.
- Класове за фигури → Управляват логиката на различни фигури (кръг, линия, триъгълник и др.).

#### 4. `managers`
Контролират класовете за фигури и служат като връзка между тях и платното.  
Грижат се за изпращането на данни към сървъра чрез сокети (`create`, `update`, `finish`).

---