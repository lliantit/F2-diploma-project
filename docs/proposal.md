# Thesis_Proposal

**Попередня робоча назва проєкту (UKR):** Розробка системи підтримки тактичних рішень у реальному часі на базі комп'ютерного зору та великих мовних моделей.
**Working Title (ENG):** Development of a Real-Time Tactical Decision Support System Based on Computer Vision and Large Language Models.

## Актуальність та проблематика

Сучасні системи спортивної відеоаналітики переважно орієнтовані на постматчевий аналіз або вимагають використання дороговартісних мультисенсорних інфраструктур із передачею даних на хмарні сервери. Це створює критичну затримку (latency) та унеможливлює отримання об'єктивної тактичної телеметрії безпосередньо під час гри для команд без доступу до Enterprise-інфраструктури. Проблема полягає у необхідності проєктування автономної мобільної системи, здатної синтезувати ігрові події (Event Data) із сирого відеопотоку та генерувати аналітичні підказки локально (Edge Computing) без залучення хмарних обчислень.

## Сформована ідея продукту

Мультимодальна програмна платформа локальної відеоаналітики (Edge Computing). Архітектура системи базується на принципі Decoupled Telemetry: роздільній екстракції координат об'єктів за допомогою згорткових нейронних мереж (YOLOv8) та подальшому їх зіставленні через евристичний рушій (State Machine Heuristics). Це дозволяє трансформувати безперервний потік фізичних координат у дискретні ігрові події. Агреговані дані аналізуються локальною LLM, яка виявляє аномалії (падіння інтенсивності, розриви ліній) та генерує текстові інсайти на планшет головного тренера.

## Детальний опис функціоналу (Core Features)

1. **Vision-Layer & Homography:** Автоматичне розпізнавання та трекінг гравців/м'яча з перетворенням піксельних координат відеопотоку у метричну 2D-площину поля.
2. **Physics Tracker:** Потоковий розрахунок індивідуальної кінематики об'єктів у реальному часі (пройдена дистанція, швидкісні зони, прискорення).
3. **Event Heuristics Engine:** Алгоритмічний синтез ігрових подій (володіння, передачі, перехоплення) на основі перетину просторово-часових векторів гравців та м'яча.
4. **AI Tactical Insights:** Генерація предиктивних підказок (наприклад, індекс втоми гравців) за допомогою локальної LLM (Phi-3.5/Llama 3) шляхом порівняння поточної телеметрії з еталонними профілями.
5. **Coach's Live Dashboard:** Реактивний мобільний інтерфейс (Android) для візуалізації теплових карт і стрічки подій через WebSocket-з'єднання з нульовою затримкою.
6. **Data Tagging API:** Асинхронний інтерфейс асистента для ручного вводу контекстних даних (фоли, картки) із подальшим їх злиттям (Sensor Fusion) з телеметрією від камери.

## Інструментарій та технологічний стек

- **Мови програмування:** Python 3.13 (Backend/AI), Kotlin (Android Client).
- **Архітектура та патерни:** Edge Computing, Clean Architecture, State Machine, Sensor Fusion, MVVM (Client).
- **AI & Computer Vision:** YOLOv8 (Ultralytics), OpenCV, NumPy, локальний LLM Inference (Ollama).
- **Backend & API:** FastAPI (REST API для історичних даних, WebSockets для live-телеметрії).
- **Бази даних:** MongoDB (документо-орієнтоване збереження Event Data у форматі JSON), SQLite (локальні еталонні профілі), Room (Android).
- **DevOps & Observability:** Docker (контейнеризація бекенду), GitHub Actions (CI/CD конвеєр), SonarQube (статичний аналізатор коду для контролю технічного боргу).

### Фінальний відформатований варіант (Українською мовою)

**Попередня робоча назва проєкту:** Розробка системи підтримки тактичних рішень у реальному часі на базі комп'ютерного зору та великих мовних моделей.

**Актуальність та проблематика:**

Сучасні платформи спортивної телеметрії вимагають дороговартісних стаціонарних мультисенсорних систем та хмарних обчислень, що створює високу мережеву затримку (latency) і унеможливлює оперативну підтримку рішень у польових умовах (Edge-середовищі). Інженерна проблема полягає у необхідності проєктування автономної високопродуктивної системи, здатної в реальному часі дешифрувати неструктурований відеопотік у стандартизовані подієві дані (Event Data) з мінімальним використанням обчислювальних ресурсів.

**Сформована ідея продукту:**
Мультимодальна подієво-орієнтована (Event-Driven) платформа локальної відеоаналітики на базі парадигми Edge Computing з ізоляцією доменного ядра за Clean Architecture. Система використовує принцип Decoupled Telemetry: незалежні потоки просторових координат гравців і м'яча екстрагуються нейромережею YOLOv8, трансформуються через матрицю гомографії та обробляються детермінованим скінченним автоматом (State Machine Heuristics) для синтезу ігрових подій. Локальна велика мовна модель (LLM) виступає аналітичним рушієм, що порівнює поточні метрики з історичним профілем у БД та асинхронно доставляє тактичні інсайти на мобільний клієнт тренера.

**Детальний опис функціоналу (Core Features):**

1. **Vision & Homography Pipeline:** Потокова детекція та трекінг об'єктів у відеопотоці з проективним перетворенням піксельних координат у метричну 2D-площину ігрового поля.
2. **Real-Time Kinematics Tracker:** Векторний розрахунок локомоторних показників (швидкість, прискорення, дистанція за швидкісними зонами) у реальному часі.
3. **Heuristic Event Synthesis Engine:** Автоматична генерація стандартизованих JSON-подій (Event Data: паси, володіння, перехоплення, стандарти) шляхом просторово-часового зіставлення траєкторій м'яча та агентів.
4. **Sensor Fusion & Tagging API:** Асинхронний шлюз для інтеграції ручних тегів від асистентів (фоли, картки) із автоматичною телеметрією комп'ютерного зору.
5. **Local LLM Tactical Advisor:** Генерація контекстних рекомендацій та виявлення тактичних аномалій (просідання ліній, індекс втоми) за допомогою локального інференсу LLM без виходу в зовнішню мережу.
6. **Reactive Coach Dashboard:** Мобільний застосунок (Android) для візуалізації 2D-радару, теплових карт та прийому WebSocket-стрімів із мінімальною затримкою.

**Попередній інструментарій та технологічний стек:**
— **Мови програмування:** Python 3.13 (Backend, CV, AI), Kotlin (Android Client).
— **Архітектурні патерни:** Clean Architecture, Event-Driven Architecture, CQRS, State Machine, MVVM (Client).
— **Фреймворки та бібліотеки:** FastAPI, WebSockets, Ultralytics YOLOv8, OpenCV, NumPy, SciPy, Ollama (Local LLM inference), Jetpack Compose.
— **Бази даних:** MongoDB (збереження високочастотної телеметрії та JSON Event Data), SQLite (еталонні профілі), Room (локальне кешування на клієнті).
— **DevOps, Security та Observability:** Docker, GitHub Actions (CI/CD), SonarQube (контроль якості коду та технічного боргу), Trivy (аудит безпеки контейнерів), k6 (навантажувальне тестування WebSocket API), Prometheus + Grafana (моніторинг FPS та latency).

### Final Formatted Version (English)

**Working Title:** Development of a Real-Time Tactical Decision Support System Based on Computer Vision and Large Language Models.

**Relevance and Problem Statement:**

Modern sports telemetry platforms rely heavily on expensive stationary multi-sensor infrastructures and cloud computing, introducing critical network latency and preventing real-time decision support in field conditions (Edge environments). The core software engineering challenge lies in designing an autonomous, high-throughput system capable of decoding unstructured video streams into standardized Event Data in real time under constrained local computing resources.

**Product Concept:**
A multimodal, Event-Driven local video analytics platform built on the Edge Computing paradigm with domain core isolation following Clean Architecture principles. The system implements Decoupled Telemetry: independent spatial coordinate streams for players and the ball are extracted via YOLOv8, projected onto a 2D plane via homography matrices, and processed by a deterministic finite state machine (State Machine Heuristics) to synthesize discrete game events. A locally hosted Large Language Model (LLM) acts as the reasoning engine, cross-referencing live telemetry against historical baseline profiles to asynchronously push tactical insights to the coach's mobile dashboard.

**Core Features:**

1. **Vision & Homography Pipeline:** Real-time object detection and tracking with projective transformation of pixel coordinates into a metric 2D pitch plane.
2. **Real-Time Kinematics Tracker:** Vector-based calculation of locomotor metrics (velocity, acceleration, speed zone distances) in real time.
3. **Heuristic Event Synthesis Engine:** Automated generation of standardized JSON Event Data (passes, possession, interceptions, set pieces) via spatiotemporal cross-referencing of ball and agent trajectories.
4. **Sensor Fusion & Tagging API:** Asynchronous gateway merging manual assistant tags (fouls, cards) with automated computer vision telemetry.
5. **Local LLM Tactical Advisor:** Context-aware tactical anomaly detection (line gaps, fatigue indices) powered by local LLM inference with zero external network dependency.
6. **Reactive Coach Dashboard:** Low-latency Android application rendering live 2D radar, heatmaps, and AI event feeds over WebSockets.

**Technology Stack:**
— **Programming Languages:** Python 3.13 (Backend, CV, AI), Kotlin (Android Client).
— **Architectural Patterns:** Clean Architecture, Event-Driven Architecture, CQRS, Finite State Machine, MVVM.
— **Frameworks & Libraries:** FastAPI, WebSockets, Ultralytics YOLOv8, OpenCV, NumPy, SciPy, Ollama (Phi-3.5 / Llama 3), Jetpack Compose.
— **Databases:** MongoDB (time-series telemetry & JSON Event Data), SQLite (baseline profiles), Room (client-side persistence).
— **DevOps, Security & Observability:** Docker, GitHub Actions (CI/CD), SonarQube (static code analysis & technical debt control), Trivy (container security scanning), k6 (WebSocket load testing), Prometheus + Grafana (inference latency & FPS observability).