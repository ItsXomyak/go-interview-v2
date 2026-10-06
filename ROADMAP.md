# Go Backend Interview Roadmap

Единый список тем и вопросов для подготовки к собеседованию на Go backend-разработчика (Middle+/Senior), включая бигтех. Дубли объединены. Порядок работы: сначала отвечаешь сам, потом сверяешься с ответом или источником.

**Обозначения**
- `[ ]` → `[x]` — когда можешь ответить вслух, без подсказок
- ⭐ — Senior / углублённый уровень, на первом проходе можно пропустить
- ✅ — у блока есть готовые ответы в `answers/`: вопрос — ссылка, нажми и попадёшь к ответу
- 📚 [Глоссарий](answers/glossary.md) — краткие описания терминов (netpoller, G-M-P, escape analysis…); в ответах термины — ссылки на него
- 📖 — где читать · 🛠 — практика по теме · 🌐 — внешний источник

**Практика**
- **P** — [go-interview-practice](https://github.com/RezaSi/go-interview-practice): `ch-N` = папка `challenge-N`, задачи с тестами
- **GI** — [goavengers/go-interview](https://github.com/goavengers/go-interview) — вопросы с ответами (RU)
- **GCE** — [go-concurrency-exercises](https://github.com/loong/go-concurrency-exercises) — задачи на конкурентность с тестами
- **TIH** — [Tech Interview Handbook](https://www.techinterviewhandbook.org/) (EN): алгоритмы, behavioral, резюме, переговоры
- Внешние ссылки проверены на доступность (октябрь 2026); сводный список — в разделе «Ресурсы» в конце

**Как проходить:** тема → ответить на вопросы сам → сверить → практика 🛠 → следующая тема. Этапы 1–2 по порядку, дальше можно параллелить. Алгоритмы (6.1) решай параллельно с теорией с первого дня, по 1–2 задачи в день.

**Правило глубины** (по фидбеку с реального собеса: «знания теоретические — нужно уметь применять»). Для каждой концепции ответь себе:
1. Что это (определение своими словами)?
2. Какую проблему решает?
3. Как устроено внутри?
4. Когда применять и когда нет?
5. Какие ограничения и trade-off?
6. Пример из практики или придуманный кейс.

Если не можешь ответить на пункты 2–6 — тема не закрыта, даже если определение помнишь.

---

<a id="stage-1"></a>
## Этап 1. Язык Go

<a id="s1-1"></a>
### 1.1 Базовые типы и синтаксис
📖 ✅ [**Ответы на весь блок**](answers/1.1-basics.md) · [GI · README](https://github.com/goavengers/go-interview/blob/master/README.md) · [GI · podolsky](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md) · 🌐 [Go Spec](https://go.dev/ref/spec)

- [ ] [Чем Go отличается от других языков (Java, Python)? Почему его выбирают для backend?](answers/1.1-basics.md#q1-1-01)
- [ ] [Технологические преимущества и недостатки Go](answers/1.1-basics.md#q1-1-02)
- [ ] ⭐ [Что огорчает в системе типов Go?](answers/1.1-basics.md#q1-1-03)
- [ ] [Go — императивный или декларативный? В чём разница?](answers/1.1-basics.md#q1-1-04)
- [ ] [Какие типы есть в Go (целые, float, complex, string, bool, составные)?](answers/1.1-basics.md#q1-1-05)
- [ ] [Что такое zero value? Нулевые значения всех типов](answers/1.1-basics.md#q1-1-06)
- [ ] [`var x int`, `x := 0`, `new(int)` — в чём разница?](answers/1.1-basics.md#q1-1-07)
- [ ] [`new` vs `make`](answers/1.1-basics.md#q1-1-08)
- [ ] [Отличия `int`, `int32`, `int64`. Чем `int` отличается от `uint`? От чего зависит размер `int`?](answers/1.1-basics.md#q1-1-09)
- [ ] [Сколько памяти занимают `int32`/`int64`, их предельные значения? Что при переполнении?](answers/1.1-basics.md#q1-1-10)
- [ ] ⭐ [Почему `len` возвращает `int`, а не `uint`?](answers/1.1-basics.md#q1-1-11)
- [ ] [Что будет при делении int на 0 и float на 0?](answers/1.1-basics.md#q1-1-12)
- [ ] [Преобразования между строками и числами (`strconv`). Можно ли сделать `string(int)` и `int(string)`?](answers/1.1-basics.md#q1-1-13)
- [ ] [Константы: можно ли изменить? Типизированные vs нетипизированные](answers/1.1-basics.md#q1-1-14)
- [ ] [Что такое `iota`? Как сделать enum?](answers/1.1-basics.md#q1-1-15)
- [ ] [Shadowing переменных — что это и чем опасно?](answers/1.1-basics.md#q1-1-16)
- [ ] [Модификаторы доступа (экспортируемые имена)](answers/1.1-basics.md#q1-1-17)
- [ ] [`type A B` vs `type A = B`](answers/1.1-basics.md#q1-1-18)
- [ ] [Что делает `_` (blank identifier)?](answers/1.1-basics.md#q1-1-19)
- [ ] [Какие циклы есть в Go? Как завершить `for` без условия? `break`/`continue` с меткой, `goto`](answers/1.1-basics.md#q1-1-20)
- [ ] [Что изменилось в циклах `for` в Go 1.22 (переменная цикла, `range int`)?](answers/1.1-basics.md#q1-1-21)
- [ ] [Как устроен `switch` (fallthrough, switch без выражения)?](answers/1.1-basics.md#q1-1-22)
- [ ] [Порядок выполнения логических операций, short-circuit. `true && !false`? `(true && false) || (false && true) || !(false && false)`?](answers/1.1-basics.md#q1-1-23)
- [ ] [Пакет `fmt`: `Println`, `Printf`, `Sprintf`, `Scan`; основные verbs (`%v`, `%+v`, `%T`)](answers/1.1-basics.md#q1-1-24)
- [ ] [Пакеты: как создавать и импортировать? Порядок инициализации пакета](answers/1.1-basics.md#q1-1-25)

🛠 P: ch-1, ch-18

<a id="s1-2"></a>
### 1.2 Строки, руны, байты
📖 ✅ [**Ответы на весь блок**](answers/1.2-strings.md) · [GI · golang #1–2](https://github.com/goavengers/go-interview/blob/master/docs/golang/README.md)

- [ ] [Как устроена строка? Почему immutable, почему нельзя `s[0] = 'a'`?](answers/1.2-strings.md#q1-2-01)
- [ ] [Что такое `rune` и `byte`?](answers/1.2-strings.md#q1-2-02)
- [ ] [Как в UTF-8 кодируется, сколькими байтами описан конкретный символ?](answers/1.2-strings.md#q1-2-03)
- [ ] [Длина строки в байтах и в символах: что вернёт `len("привет")`? `utf8.RuneCountInString`](answers/1.2-strings.md#q1-2-04)
- [ ] [Как работает `range` по строке? Чем отличается от итерации по индексу?](answers/1.2-strings.md#q1-2-05)
- [ ] [Что происходит при конкатенации? Как эффективно склеивать много строк (`strings.Builder`, `bytes.Buffer`, `strings.Join`)?](answers/1.2-strings.md#q1-2-06)
- [ ] [Конвертация `string ↔ []byte` — всегда ли копирование?](answers/1.2-strings.md#q1-2-07)
- [ ] [Пакет `strings`: основные функции; новое в `strings`/`bytes`](answers/1.2-strings.md#q1-2-08)

🛠 RLE-сжатие · P: ch-2, ch-17, ch-23, ch-26

<a id="s1-3"></a>
### 1.3 Массивы и слайсы
📖 ✅ [**Ответы на весь блок**](answers/1.3-slices.md) · [GI · README](https://github.com/goavengers/go-interview/blob/master/README.md) · 🌐 [Go Blog: Slices internals](https://go.dev/blog/slices-intro)

- [ ] [Массив vs слайс. Массив — значение: что из этого следует?](answers/1.3-slices.md#q1-3-01)
- [ ] [Как устроен слайс (ptr, len, cap)? Сколько весит заголовок слайса?](answers/1.3-slices.md#q1-3-02)
- [ ] [Способы создать слайс. nil-слайс vs пустой слайс; можно ли `append` в nil? Как проверить на пустоту?](answers/1.3-slices.md#q1-3-03)
- [ ] [Как работает `append` и рост capacity (старая и новая формула)? Можно ли `append` к массиву? Напиши свой `append`](answers/1.3-slices.md#q1-3-04)
- [ ] [Общий базовый массив: когда изменение одного слайса видно в другом?](answers/1.3-slices.md#q1-3-05)
- [ ] [Слайс передан в функцию: изменится ли он снаружи при изменении элемента? А при `append`?](answers/1.3-slices.md#q1-3-06)
- [ ] [Реслайсинг `s[a:b]`; полное выражение `s[a:b:c]` — зачем?](answers/1.3-slices.md#q1-3-07)
- [ ] [Как скопировать слайс (`copy`, трюк с `append`)? Как слить два слайса?](answers/1.3-slices.md#q1-3-08)
- [ ] [Удаление элемента с сохранением порядка и без](answers/1.3-slices.md#q1-3-09)
- [ ] [Удалить дубликаты из слайса без переаллокации — можно ли?](answers/1.3-slices.md#q1-3-10)
- [ ] [Как сделать из слайса массив?](answers/1.3-slices.md#q1-3-11)
- [ ] [Что лучше — связный список или массив? Почему (локальность, кэш CPU)?](answers/1.3-slices.md#q1-3-12)
- [ ] [Big-O всех операций со слайсом](answers/1.3-slices.md#q1-3-13)
- [ ] [Утечка памяти через подслайс — как избежать?](answers/1.3-slices.md#q1-3-14)
- [ ] [Пакет `slices` (Go 1.21+)](answers/1.3-slices.md#q1-3-15)
- [ ] [Как отсортировать слайс структур по полю (`sort.Slice`, `slices.SortFunc`)?](answers/1.3-slices.md#q1-3-16)

🛠 Two Sum · Пересечение слайсов · P: ch-19

### 1.4 Map и хеш-таблицы
📖 [GI · podolsky #6–7](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md)

- [ ] Как работает хеш-таблица? Что такое хеш-функция?
- [ ] Методы разрешения коллизий (цепочки, открытая адресация)
- [ ] Как устроена map в Go под капотом (классическая: `hmap`, бакеты)? Сколько элементов в бакете?
- [ ] Что такое эвакуация, когда она происходит и как её избежать?
- [ ] ⭐ Map на Swiss Tables (Go 1.24+): чем отличается от старой реализации?
- [ ] Как происходит поиск по ключу?
- [ ] Какая хеш-функция используется в map?
- [ ] Что вернётся по несуществующему ключу? Как проверить наличие ключа?
- [ ] Чтение и запись в nil-map
- [ ] Что может быть ключом map?
- [ ] Почему порядок итерации по map случайный?
- [ ] Почему нельзя взять адрес элемента `&m[k]`? Как изменить поле структуры, лежащей в map?
- [ ] Освобождает ли `delete` память? Как избежать утечек памяти в слайсах и map?
- [ ] Big-O операций с map
- [ ] Сколько весят слайс, map, пустая строка, int?
- [ ] ⭐ Как реализовать разреженный массив на Go?

🛠 Group Anagrams · Top K · P: ch-6

### 1.5 Функции, методы, замыкания, defer

- [ ] Зачем нужны функции? Функции как значения (first-class)
- [ ] Чем полезны анонимные и вариативные функции?
- [ ] Замыкание: что это, примеры, где полезно
- [ ] Рекурсия: примеры, какие проблемы (глубина стека, производительность)?
- [ ] Передача аргументов: по значению или по ссылке? Какие типы ведут себя как ссылки?
- [ ] Функция vs метод. Как создать свой метод? Можно ли объявить метод на типе из другого пакета?
- [ ] Value receiver vs pointer receiver — когда что? Method set
- [ ] Функция `init`: зачем нужна, порядок вызова
- [ ] `defer`: зачем, порядок вызова, когда вычисляются аргументы
- [ ] Захват значений переменных в `defer`; `defer` и именованный результат
- [ ] Как вернуть ошибку изнутри `defer` (не просто залогировать)?
- [ ] ⭐ Функциональные опции (functional options)
- [ ] Напиши `swap(&x, &y)`


### 1.6 Структуры, интерфейсы, указатели
📖 [GI · README](https://github.com/goavengers/go-interview/blob/master/README.md) · [GI · podolsky #2–3, #13, #25](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md) · 🌐 [Russ Cox: Go Data Structures: Interfaces](https://research.swtch.com/interfaces)

- [ ] Что такое структура, зачем? Теги структур
- [ ] Можно ли сравнивать структуры? Пустая структура `struct{}` — зачем?
- [ ] Чем пустой интерфейс отличается от пустой структуры? Почему в канал-сигнал передают `struct{}`, а не `interface{}`?
- [ ] ⭐ Почему два `new(struct{})` могут иметь одинаковый адрес?
- [ ] Выравнивание полей (alignment/padding), размер структуры
- [ ] Что такое указатели? Когда их использовать?
- [ ] Что такое интерфейс? Утиная типизация; чем отличается от интерфейсов в Java/PHP?
- [ ] Неявная реализация интерфейсов — плюсы и минусы. Как заставить компилятор проверить, что тип реализует интерфейс?
- [ ] Интерфейс как структура: `iface`, `eface`, `itab`
- [ ] Пустой интерфейс, `any` — когда использовать?
- [ ] nil-интерфейс ≠ интерфейс с nil-значением. Как вызов метода на интерфейсе, не равном nil, может упасть с nil pointer dereference?
- [ ] Почему говорят, что у nil в Go есть тип? Как получить переменную, которая «не nil, но nil»?
- [ ] Сравнение интерфейсов
- [ ] Type assertion и `switch v := x.(type)`: способы применения
- [ ] ⭐ Тип-сумма: что это и как реализовать на Go?
- [ ] Где объявлять интерфейс: на стороне потребителя или реализации? Почему?
- [ ] Embedding — это наследование? Почему нет?
- [ ] Почему нельзя копировать структуру с `sync.Mutex` внутри? Как это ловит `go vet`?
- [ ] ⭐ Когда интерфейс вызывает аллокацию?
- [ ] Сериализация: что это, зачем; JSON-теги, неэкспортируемые поля
- [ ] Реализуй интерфейс площади для `Circle` и `Square`

🛠 задача МТС на выравнивание структур · P: ch-3, ch-10

### 1.7 Ошибки, panic, recover
📖 [GI · podolsky #14](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md)

- [ ] Что такое `error`? Как правильно обрабатывать ошибки?
- [ ] Sentinel errors, кастомные типы ошибок, обёртки — когда что?
- [ ] Зачем врапать ошибки? Способы врапинга (`%w`, свой тип с `Unwrap`)
- [ ] `errors.Is` vs `errors.As` vs `==`; `errors.AsType`
- [ ] Несколько ошибок сразу (`errors.Join`)
- [ ] Recoverable vs fatal ошибки: как это сделано в пакете `net` и как делать в современном Go?
- [ ] Что такое panic? Когда её использовать? Что будет при `panic(nil)`?
- [ ] Как работает `recover`? Поймает ли он панику из другой горутины? Что нельзя поймать?
- [ ] ⭐ Чем отличаются panic, fatal error и throw? Почему конкурентная запись в map роняет процесс так, что `recover` не поможет?
- [ ] Порядок выполнения при панике
- [ ] Ошибка в `defer f.Close` — теряем? Как не потерять?

🛠 P: ch-7, ch-12

### 1.8 Дженерики
📖 [GI · podolsky #26](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md)

- [ ] Какие средства обобщённого программирования есть в Go?
- [ ] Синтаксис и constraints; `comparable`, `~T`, union-типы
- [ ] Как реализованы дженерики (GC shape stenciling)? Есть ли оверхед?
- [ ] Дженерики или интерфейсы — когда что?
- [ ] Что нельзя делать с дженериками?
- [ ] Инференс типов
- [ ] ⭐ Как заставить generic-функцию вызывать методы с pointer receiver и при этом принимать `[]T`?
- [ ] ⭐ Итераторы range-over-func (Go 1.23), `iter.Pull`
- [ ] ⭐ Параметризованные алиасы (1.24), самоссылающиеся ограничения (1.26), generic-методы (1.27)

🛠 LRU Cache · P: ch-27

### 1.9 Стандартная библиотека и тулинг
📖 🌐 [Effective Go](https://go.dev/doc/effective_go) · 🌐 [pkg.go.dev/std](https://pkg.go.dev/std) · 🌐 [100 Go Mistakes](https://100go.co/) · 🌐 [uproger: Go 1.27 — 20 примеров](https://uproger.com/go-1-27-20-gotovyh-primerov-s-kodom-dlya-prodvinutogo-razrabotchika/) (⚠️ статья помечает все примеры как «Go 1.27», хотя большинство API появились раньше)

- [ ] `io.Reader` / `io.Writer`: зачем, как композируются (`io.Copy`, `io.TeeReader`, `io.MultiWriter`, `io.LimitReader`)?
- [ ] `bufio`: когда нужен и почему быстрее?
- [ ] Работа с файлами: `os.Open` vs `os.ReadFile`, закрытие, чтение большого файла построчно
- [ ] `time`: `Duration`, таймзоны, `time.After` в цикле, зачем `Ticker.Stop`, переиспользование таймера через `Reset`
- [ ] `encoding/json`: теги, `omitempty`, `json.RawMessage`, потоковый `json.Decoder`; почему медленный и чем заменить?
- [ ] JSON, где поле приходит то строкой, то числом: как написать десериализатор (`UnmarshalJSON`)?
- [ ] `net/http` клиент: почему клиент надо переиспользовать, зачем закрывать и дочитывать `resp.Body`, пул соединений в `Transport`
- [ ] Как ограничить размер ответа внешнего сервиса и тела запроса (`io.LimitReader`, `http.MaxBytesReader`)?
- [ ] `os.Root`: безопасная работа с файлами внутри каталога (защита от path traversal)
- [ ] `container/heap`, `container/list` — когда пригодятся?
- [ ] `golang.org/x/sync`: `errgroup`, `semaphore`, `singleflight`
- [ ] `go vet`, `staticcheck`, `golangci-lint`, `gofmt` / `goimports`
- [ ] `//go:embed`, build tags (`//go:build`), `go generate`
- [ ] Кросс-компиляция (`GOOS`/`GOARCH`), `CGO_ENABLED=0`

---

<a id="stage-2"></a>
## Этап 2. Конкурентность и runtime

### 2.1 Потоки, горутины, планировщик
> Планировщик на собесах спрашивают особенно подробно.

📖 🌐 Ardan Labs: [Scheduling in Go I](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part1.html), [II](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part2.html)

- [ ] Что такое процесс и поток ОС?
- [ ] Что такое системный вызов? Сетевой вызов?
- [ ] Конкурентность vs параллелизм
- [ ] Что такое горутина? Горутина vs поток ОС. Сколько памяти занимает, как растёт стек?
- [ ] Типы многозадачности: вытесняющая и кооперативная. Какая в Go сейчас и какая была до 1.14?
- [ ] Переключение контекста: что происходит, почему у потоков дороже, чем у горутин?
- [ ] Каковы функции планировщика?
- [ ] Модель G-M-P: что такое G, M, P; локальная и глобальная очереди, `runnext`
- [ ] Есть ли в Go thread pool? Какого он размера и зачем нужен?
- [ ] Work stealing
- [ ] Что происходит при блокирующем системном вызове (hand off P)? Что такое netpoller?
- [ ] Что происходит, когда горутина отправляет данные в сетевое соединение?
- [ ] Вытеснение (preemption): кооперативное и асинхронное (sysmon, `SIGURG`)
- [ ] Какие бывают состояния у горутин?
- [ ] `GOMAXPROCS`; поведение в контейнерах (Go 1.25)
- [ ] `runtime.Gosched`, `runtime.Goexit`, `LockOSThread`
- [ ] Сколько горутин можно запустить? Что ограничивает?
- [ ] ⭐ Как получить ID текущей горутины, если API для этого нет? Почему его не дают?
- [ ] ⭐ Что делает `sysmon`?

### 2.2 Каналы и select
📖 [GI · golang #8–10, #22](https://github.com/goavengers/go-interview/blob/master/docs/golang/README.md)

- [ ] Что такое канал и зачем нужен? Как устроен (`hchan`)?
- [ ] Буферизированный vs небуферизированный канал. Как создать, закрыть, задать направление?
- [ ] Чтение / запись / закрытие для nil-канала, открытого и закрытого — что будет в каждом случае?
- [ ] Кто должен закрывать канал? Что будет, если закрыть закрытый канал?
- [ ] Что будет, если отправить в канал, у которого нет читателей?
- [ ] Как работает `select`? Порядок выбора, `default`, nil-каналы в `select`
- [ ] Как сделать неблокирующее чтение из канала?
- [ ] Какой канал быстрее передаст значение: буферизированный или небуферизированный?
- [ ] Как сделать таймаут на операцию (`select` + `time.After` / `context`)?
- [ ] Что такое deadlock? Когда рантайм его ловит?
- [ ] Goroutine leak: что это, как найти (профиль `goroutineleak`) и предотвратить?
- [ ] Как дождаться завершения горутин? Как остановить горутину извне?
- [ ] Как ограничить число одновременных горутин?
- [ ] Паттерны: generator, fan-in, fan-out, pipeline, worker pool, semaphore, pub/sub, or-done, tee
- [ ] Каналы или мьютексы — когда что?
- [ ] Можно ли реализовать `sync.Mutex` и `sync.WaitGroup` на каналах? Как?
- [ ] Напиши свой `Sleep` через `time.After`
- [ ] ⭐ Как работает `select` внутри? Что изменилось в таймерах в Go 1.23?

🛠 Worker Pool · Fan-in · Pipeline · Первый ответ из N · [GI · popular_tasks #2–6](https://github.com/goavengers/go-interview/blob/master/docs/popular_tasks/README.md) · P: ch-4, ch-8, ch-11 · [GCE](https://github.com/loong/go-concurrency-exercises): 0-limit-crawler, 1-producer-consumer, 3-limit-service-time

### 2.3 sync, atomic, модель памяти
📖 [GI · podolsky #18–20](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md) · 🌐 [The Go Memory Model](https://go.dev/ref/mem)

- [ ] Что такое race condition? Чем отличается от data race? Как найти (`-race`)?
- [ ] Какие способы синхронизации есть в Go?
- [ ] `sync.Mutex`: как устроен? Какие типы мьютексов есть в stdlib?
- [ ] Что именно защищает мьютекс?
- [ ] ⭐ Нормальный режим и режим голодания (starvation mode) у `sync.Mutex`
- [ ] `Mutex` vs `RWMutex`; когда `RWMutex` выгоден?
- [ ] Сколько R- и W-локов можно взять от `RWMutex` одновременно? Что будет, если взять `Lock`, не отпустив `RLock`?
- [ ] Особенности работы с map в горутинах: что будет при конкурентной записи, как защититься?
- [ ] `sync.Map`: как устроена, какие недостатки? Что лучше: map + mutex или `sync.Map`?
- [ ] `sync.WaitGroup` (и `wg.Go`, Go 1.25); `sync.Once`, `OnceFunc`, `OnceValue`
- [ ] `sync.Cond` — зачем, если есть каналы?
- [ ] `sync.Pool`
- [ ] Зачем нужны atomic? Что умеет `sync/atomic` (в т.ч. `atomic.Pointer`), когда он лучше мьютекса?
- [ ] Почему интенсивная конкурентная запись в один atomic заметно тормозит?
- [ ] ⭐ Что обычно быстрее: atomic, mutex или каналы?
- [ ] Модель памяти Go, happens-before
- [ ] Можно ли использовать один буфер `[]byte` в нескольких горутинах?
- [ ] Можно ли захватить мьютекс с таймаутом?
- [ ] Как тестировать конкурентный код без `time.Sleep`?
- [ ] ⭐ False sharing
- [ ] ⭐ Lock-free структуры данных, CAS, проблема ABA. Есть ли такое в Go?
- [ ] ⭐ Copy-on-write конфиг: обновление без блокировок на чтении

🛠 Кэш с TTL · Pub/Sub · Singleflight · ⭐Шардированная map · ⭐Lock-free стек · [GCE](https://github.com/loong/go-concurrency-exercises): 2-race-in-cache, 5-session-cleaner

### 2.4 context

- [ ] Зачем нужен `context`? Какие методы у интерфейса?
- [ ] Чем отличаются все виды контекста: `Background`, `TODO`, `WithCancel`, `WithTimeout`, `WithDeadline`, `WithValue`, `WithCancelCause`, `WithoutCancel`, `AfterFunc`?
- [ ] Примеры применения каждого вида
- [ ] Почему обязательно вызывать `cancel`?
- [ ] Правила использования (первый аргумент, не хранить в структуре, что можно класть в `Value`)
- [ ] Как работает `Value` и почему он медленный?
- [ ] Как отмена доходит до HTTP-клиента и БД?
- [ ] Как проверять отмену в горячем цикле?

🛠 ⭐errgroup с лимитом · P: ch-30

### 2.5 Память и GC
📖 [GI · golang #17, #21](https://github.com/goavengers/go-interview/blob/master/docs/golang/README.md) · 🌐 [A Guide to the Go GC](https://go.dev/doc/gc-guide)

- [ ] Как работает стек? Как работает куча? Что быстрее и почему?
- [ ] Escape analysis: как понять, что переменная утекает в кучу (`-gcflags=-m`)?
- [ ] Как устроен аллокатор (mcache, mcentral, mheap)?
- [ ] Какой алгоритм реализует сборщик мусора Go?
- [ ] Что такое stop the world и сколько раз за цикл GC он происходит?
- [ ] Сколько ресурсов требует GC? Можно ли предсказать, что он отработает за константное время?
- [ ] `GOGC` и `GOMEMLIMIT`
- [ ] Как снизить нагрузку на GC?
- [ ] Какие бывают утечки памяти в Go при наличии GC?
- [ ] ⭐ Green Tea GC
- [ ] ⭐ Hybrid write barrier
- [ ] ⭐ Финализаторы, `runtime.AddCleanup`, пакеты `unique` и `weak`

### 2.6 ⭐ Продвинутый runtime, компилятор, unsafe

- [ ] Инлайнинг: как работает, как контролировать?
- [ ] Девиртуализация: когда компилятор превращает вызов через интерфейс в прямой?
- [ ] Bounds check elimination
- [ ] PGO (Profile-Guided Optimization)
- [ ] Какие директивы компилятора нужно знать?
- [ ] Как посмотреть, во что скомпилировался код?
- [ ] Правила `unsafe.Pointer`; `[]byte ↔ string` без копирования
- [ ] Рефлексия: зачем нужна, почему к ней настороженное отношение, где без неё не обойтись? Насколько дорог reflect? Как проверить тип переменной в runtime?
- [ ] Чем опасен cgo?
- [ ] Почему на Go почти не пишут расширения для других языков и динамические библиотеки? Почему Go plugins неудобны (и Terraform выбрал плагины через gRPC)?
- [ ] `//go:linkname`: как вызвать приватную функцию другого пакета и чем это опасно?
- [ ] Как писать код без лишних аллокаций в горячем пути?
- [ ] `runtime.ReadMemStats` vs `runtime/metrics`
- [ ] Монотонное время в `time.Time`

---

<a id="stage-3"></a>
## Этап 3. Инструменты, прод, ОС

### 3.1 Модули и сборка

- [ ] Зачем нужен `go mod`? Из чего состоит `go.mod` (`module`, `go`, `toolchain`, `require`, `replace`, `exclude`, `retract`)?
- [ ] Зачем нужен `go.sum`?
- [ ] Для чего нужен `replace` в `go.mod`?
- [ ] Что значит `// indirect`?
- [ ] Workspace (`go work`)
- [ ] Линтеры: какие знаешь, какой любимый?
- [ ] ⭐ Как Go выбирает версии зависимостей (MVS)?
- [ ] ⭐ Как собрать минимальный воспроизводимый бинарник для прода?
- [ ] ⭐ Что спросят про безопасность в Go?

### 3.2 Тестирование

- [ ] Зачем необходимо тестирование ПО? Пирамида тестирования
- [ ] Unit vs integration vs e2e тесты
- [ ] Что такое mock, stub, fake, fixture?
- [ ] Как тестировать модуль, работающий с БД: unit-тесты (моки через интерфейсы) и интеграционные (testcontainers)
- [ ] White box vs black box testing
- [ ] Что такое performance testing и security testing?
- [ ] Table-driven тесты
- [ ] `t.Error` vs `t.Fatal`, `t.Helper`, `t.Cleanup`, `t.TempDir`, `t.Setenv`, `t.Context`, `t.Parallel`
- [ ] Моки в Go: gomock, mockery, ручные
- [ ] 🌐 Пакет testify: `assert`, `require`, `mock`, `suite` → [stretchr/testify](https://github.com/stretchr/testify)
- [ ] Бенчмарки; `testing.B.Loop` (Go 1.24)
- [ ] Фаззинг
- [ ] `testing/synctest` (Go 1.25)
- [ ] Покрытие тестами
- [ ] TDD: почему тесты пишутся до кода? Как тесты влияют на организацию кода?

🛠 P: ch-16

### 3.3 Observability и troubleshooting
📖 [GI · podolsky #15, #21–24](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md) · 🌐 [Go Diagnostics](https://go.dev/doc/diagnostics) · 🌐 [OpenTelemetry Concepts](https://opentelemetry.io/docs/concepts/) · 🌐 [Prometheus metric types](https://prometheus.io/docs/concepts/metric_types/) · 🌐 SRE book: [SLO](https://sre.google/sre-book/service-level-objectives/), [Monitoring](https://sre.google/sre-book/monitoring-distributed-systems/)

- [ ] Что такое мониторинг и зачем он нужен?
- [ ] Логи, метрики, трейсинг, профилирование — что это и чем отличаются?
- [ ] Инструменты мониторинга (назови минимум 3)
- [ ] Уровни логов: когда какой использовать? Структурированное логирование (`log/slog`). Главный недостаток стандартного логгера?
- [ ] Любимый логгер? Чем хороши zerolog / zap, когда хватит `slog`?
- [ ] Как не утечь секреты в логи (`slog.LogValuer`)?
- [ ] Достоинства и недостатки метрик
- [ ] Типы метрик Prometheus (counter, gauge, histogram, summary). Стандартный набор метрик в Go-программе
- [ ] ⭐ Histogram vs summary: как считаются перцентили, почему нельзя усреднять p99?
- [ ] Что можно увидеть с помощью трейсинга? Distributed tracing, OpenTelemetry, context propagation
- [ ] Что такое APM (application performance management)?
- [ ] Методики RED / USE; four golden signals
- [ ] Алертинг: на что ставить алерты (симптомы vs причины)?
- [ ] pprof: какие профили бывают, как встроить в приложение, пример использования, overhead
- [ ] Как читать flame graph?
- [ ] `go tool trace`, Flight Recorder
- [ ] Что такое debugging, breakpoint? Delve
- [ ] Что такое stdin, stdout, stderr?
- [ ] Как искать проблемы производительности на проде?
- [ ] Сервер тормозит — куда смотреть по шагам (логи, CPU и память, сеть, диск, БД, pprof)?
- [ ] Сервис ест много памяти или течёт — как расследовать по шагам?
- [ ] ⭐ p99 латентности растёт, а CPU-профиль «нормальный» — что делать?
- [ ] ⭐ Как отлаживать упавший или зависший процесс в проде?

🛠 ТЗ: Go-приложение со всеми типами метрик Prometheus + стандартные метрики (CPU, heap, memory) → графики в Grafana, всё в docker-compose

### 3.4 🌐 Операционные системы и Linux
📖 🌐 [OSTEP](https://pages.cs.wisc.edu/~remzi/OSTEP/) (главы про процессы, виртуальную память, конкурентность, персистентность) · 🌐 [Brendan Gregg: Linux Performance](https://www.brendangregg.com/linuxperf.html) · 🌐 [The USE Method](https://www.brendangregg.com/usemethod.html)

- [ ] Процесс vs поток: что у них общее, что своё? Адресное пространство процесса (text, data, heap, stack)
- [ ] Виртуальная память: страницы, page fault, TLB, swap. Почему RSS ≠ VSZ?
- [ ] User space vs kernel space; что происходит при системном вызове?
- [ ] Файловые дескрипторы; «всё есть файл»; лимит `ulimit -n` и ошибка «too many open files»
- [ ] Модели ввода-вывода: блокирующий, неблокирующий, мультиплексирование (`select` / `poll` / `epoll` / `kqueue`). Как на этом построен netpoller Go? ⭐ io_uring
- [ ] Сигналы: SIGTERM vs SIGKILL vs SIGINT vs SIGHUP; обработка в Go (`os/signal`, `signal.NotifyContext`)
- [ ] Page cache и `fsync`: почему «записанные» данные могут потеряться при падении?
- [ ] Главная проблема производительности современных систем: почему память — узкое место? Кэши CPU, cache line, локальность данных
- [ ] Zombie и orphan процессы; ⭐ PID 1 в контейнере
- [ ] cgroups и namespaces — на чём построены контейнеры
- [ ] systemd: unit-файлы, `systemctl`, `journalctl -u`
- [ ] OOM killer: когда приходит, как понять, что процесс убит им?
- [ ] Linux-инструменты: `top`/`htop`, `ps`, `lsof`, `ss`/`netstat`, `strace`, `tcpdump`, `df`/`du`, `free`, `vmstat`, `iostat`, `dmesg`, `journalctl`, `dig`, `curl`
- [ ] Как найти процесс, который занял порт? Что делать, если кончилось место на диске / дескрипторы / память?

### 3.5 Деплой, контейнеры, Kubernetes
📖 [GI · infrastructure_and_deploy](https://github.com/goavengers/go-interview/blob/master/docs/infrastructure_and_deploy/README.md) · 🌐 [Docker overview](https://docs.docker.com/get-started/docker-overview/) · 🌐 [Multi-stage builds](https://docs.docker.com/build/building/multi-stage/) · 🌐 [Обзор Kubernetes (RU)](https://kubernetes.io/ru/docs/concepts/overview/)

- [ ] Blue-green deployment
- [ ] Canary-развёртывания
- [ ] Dark и A/B-развёртывания
- [ ] Rolling update; feature flags
- [ ] SLA, SLO, SLI, error budget
- [ ] Какие инструменты CI/CD знаешь?
- [ ] Как обеспечить непрерывность и стабильность деплоя?
- [ ] С какими проблемами при деплое сталкивался, как митигировал?
- [ ] 12-factor app
- [ ] Контейнеризация vs виртуализация
- [ ] 🌐 Docker: образ vs контейнер, слои и кэш сборки, multi-stage build, `scratch` / distroless для Go
- [ ] 🌐 Kubernetes: pod, deployment, service, ingress, configmap, secret
- [ ] 🌐 Liveness vs readiness vs startup probes → [Probes](https://kubernetes.io/docs/concepts/workloads/pods/probes/)
- [ ] 🌐 Остановка пода: SIGTERM, `preStop`, grace period — как связать с graceful shutdown в Go? → [Pod termination](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination)
- [ ] Requests и limits: CPU throttling и `GOMAXPROCS`, OOMKilled и `GOMEMLIMIT`
- [ ] ⭐ HPA: как автоскейлить сервис?

### 3.6 🌐 Git
📖 🌐 [Pro Git (RU)](https://git-scm.com/book/ru/v2)

- [ ] merge vs rebase — когда что?
- [ ] `cherry-pick`; `revert` vs `reset`
- [ ] Как разрешить конфликт?
- [ ] Git flow vs trunk-based development
- [ ] ⭐ `git bisect`: как найти коммит, который сломал поведение

---

<a id="stage-4"></a>
## Этап 4. Backend

### 4.1 Сети и протоколы
📖 [GI · common](https://github.com/goavengers/go-interview/blob/master/docs/common/README.md) · 🌐 [High Performance Browser Networking](https://hpbn.co/) · 🌐 [what-happens-when](https://github.com/alex/what-happens-when)

- [ ] Уровни модели OSI (и TCP/IP)
- [ ] Какие протоколы взаимодействия приложений по сети знаешь?
- [ ] MAC-адрес vs IP-адрес; ⭐ подсети и CIDR
- [ ] TCP vs UDP; когда UDP предпочтительнее?
- [ ] 🌐 TCP: 3-way handshake, закрытие соединения, TIME_WAIT и CLOSE_WAIT (что значит много CLOSE_WAIT?)
- [ ] 🌐 Flow control vs congestion control
- [ ] Что такое сокет и порт? ⭐ `bind` / `listen` / `accept`
- [ ] Что такое NAT?
- [ ] Что такое DNS, как работает резолвинг? Что такое TTL записи?
- [ ] Что такое proxy? Forward vs reverse proxy; nginx как reverse proxy
- [ ] Что такое CDN?
- [ ] HTTP vs HTTPS; за счёт чего достигается безопасность в HTTPS?
- [ ] SSL vs TLS; 🌐 TLS 1.3 handshake, сертификаты и цепочка доверия, mTLS
- [ ] HTTP/1.1 vs HTTP/2; 🌐 HTTP/3 и QUIC — зачем?
- [ ] Keep-alive (HTTP и TCP); пул соединений
- [ ] Группы status codes
- [ ] POST vs PUT vs PATCH; идемпотентность методов; зачем нужен OPTIONS?
- [ ] 🌐 CORS; cookies: `HttpOnly`, `Secure`, `SameSite`
- [ ] Принципы REST
- [ ] Что такое WebSocket? Long polling vs WebSocket vs SSE
- [ ] gRPC vs HTTP/REST; Protobuf
- [ ] Что спрашивают про gRPC: виды стриминга, дедлайны, interceptors, коды ошибок
- [ ] 🌐 Что происходит, когда вводишь URL в браузере? (от DNS до ответа сервера)

### 4.2 HTTP-сервисы на Go

- [ ] Как устроен сервер `net/http`?
- [ ] Что умеет `ServeMux` с Go 1.22?
- [ ] Middleware: как написать?
- [ ] Валидация входящих запросов
- [ ] Таймауты сервера и клиента
- [ ] Graceful shutdown
- [ ] Логирование запросов
- [ ] JSON: `encoding/json`, `encoding/json/v2`
- [ ] Фреймворки (gin, echo, fiber) — нужны ли?

🛠 Graceful shutdown · [GCE · 4-graceful-sigint](https://github.com/loong/go-concurrency-exercises/tree/main/4-graceful-sigint) · P: ch-5, ch-9, ch-14 · [P · packages](https://github.com/RezaSi/go-interview-practice/tree/main/packages) (gin, echo, fiber)

### 4.3 🌐 Проектирование API
📖 🌐 [Google API design guide](https://docs.cloud.google.com/apis/design) · 🌐 [AIP-158: Pagination](https://google.aip.dev/158) · 🌐 [Slack: Evolving API Pagination](https://slack.engineering/evolving-api-pagination-at-slack/) · 🌐 [Stripe: Idempotent requests](https://docs.stripe.com/api/idempotent_requests)

- [ ] REST (OpenAPI) vs gRPC vs GraphQL — критерии выбора
- [ ] Ресурсная модель: именование эндпоинтов, методы, коды ответов
- [ ] Версионирование API
- [ ] Пагинация: offset vs cursor/keyset — плюсы и минусы
- [ ] Идемпотентность: как реализовать idempotency key на сервере?
- [ ] Формат ошибок; какие коды возвращать
- [ ] Обратная совместимость: что можно и нельзя менять (в т.ч. номера полей в protobuf)
- [ ] Лимиты и квоты: `429`, `Retry-After`

### 4.4 🌐 Безопасность и аутентификация
📖 🌐 [OWASP Top 10:2025](https://top10.owasp.org/2025/) · 🌐 [OWASP Password Storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html) · 🌐 [JWT Introduction](https://www.jwt.io/introduction) · 🌐 [OAuth 2.0](https://oauth.net/2/) · 🌐 [How OpenID Connect Works](https://openid.net/developers/how-connect-works/)

- [ ] Аутентификация vs авторизация
- [ ] Сессии и cookies vs токены
- [ ] JWT: структура, подпись (HS256 vs RS256), проблемы (отзыв, хранение); access + refresh токены
- [ ] OAuth 2.0: роли и flows (authorization code + PKCE, client credentials). Чем OIDC отличается от OAuth 2.0?
- [ ] Хранение паролей: соль, bcrypt / argon2id; почему не MD5 / SHA-256?
- [ ] OWASP Top 10: SQL injection, XSS, CSRF, SSRF, broken access control
- [ ] Какие сетевые атаки знаешь (MITM, DDoS, spoofing)? Как защищаться?
- [ ] Безопасные заголовки: CORS, CSP, HSTS
- [ ] mTLS между сервисами
- [ ] Где хранить секреты (Vault, K8s Secrets); почему не в git?
- [ ] RBAC vs ABAC
- [ ] Go: `crypto/rand` vs `math/rand`, `html/template` и экранирование, `govulncheck`

🛠 P: ch-15

### 4.5 SQL и реляционные БД
📖 [GI · cache_and_db](https://github.com/goavengers/go-interview/blob/master/docs/cache_and_db/README.md)

- [ ] Что означает SQL? Какая БД является реляционной?
- [ ] Базовые команды SQL (DDL, DML)
- [ ] Что такое схема в БД?
- [ ] `ORDER BY`, `LIMIT X OFFSET Y` (и почему OFFSET плох на больших таблицах), `DISTINCT`
- [ ] `GROUP BY`, агрегатные функции, `HAVING`; WHERE vs HAVING; можно ли HAVING без группировки?
- [ ] Виды JOIN; JOIN с подзапросами; коррелированный подзапрос; `EXISTS` vs `IN`
- [ ] `UNION` vs `UNION ALL`
- [ ] `INSERT ... ON CONFLICT` (upsert), `RETURNING`
- [ ] Виды связей между таблицами; как реализовать many-to-many?
- [ ] Нормализация, первые 3 НФ. Когда нужна денормализация?
- [ ] Аномалии ненормализованной схемы — вставки, обновления, удаления: покажи на примере таблицы `orders`, где хранятся данные клиента
- [ ] Какую проблему решает нормализация и чем за неё платим (JOIN'ы, сложнее запросы)? Денормализация на примере: как держать копии данных консистентными?
- [ ] `DELETE FROM table` vs `TRUNCATE TABLE`
- [ ] Что такое view? ⭐ Materialized view
- [ ] Что такое триггер?
- [ ] Зачем нужен `WITH ... AS` (CTE)?
- [ ] Зачем нужны оконные функции?
- [ ] 🌐 Дорог ли `SELECT COUNT(*)` в PostgreSQL? Какие есть более быстрые альтернативы? → [PG wiki: Count estimate](https://wiki.postgresql.org/wiki/Count_estimate)
- [ ] NULL: когда использовать, когда избегать
- [ ] Выбор типов данных: целые, DECIMAL vs FLOAT, VARCHAR vs CHAR vs TEXT, DATETIME vs TIMESTAMP, ENUM
- [ ] 🌐 Oracle: package → [PL/SQL Packages](https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/plsql-packages.html); heterogeneous calls → [Heterogeneous Services](https://docs.oracle.com/en/database/oracle/oracle-database/19/heter/heterogeneous-services-role.html); virtual table → [Overview of Views](https://docs.oracle.com/en/database/oracle/oracle-database/19/cncpt/partitions-views-and-other-schema-objects.html#GUID-15E7AEDB-9A3F-4B31-AD2D-66253CC822E5)
- [ ] ⭐ InnoDB vs MyISAM (MySQL)

🛠 Писать SQL руками (JOIN, GROUP BY, оконные функции): 🌐 [pgexercises.com](https://pgexercises.com/) · 🌐 [sql-ex.ru](https://sql-ex.ru/)

### 4.6 Индексы
📖 [GI · cache_and_db](https://github.com/goavengers/go-interview/blob/master/docs/cache_and_db/README.md) · 🌐 [PG: Index Types](https://www.postgresql.org/docs/current/indexes-types.html) · 🌐 [PG: Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html) ([RU](https://postgrespro.ru/docs/postgresql/current/using-explain))

- [ ] Что такое индекс? Как он устроен внутри (B-tree, hash)?
- [ ] Плюсы и минусы индексов. Почему не создавать индексы на все столбцы?
- [ ] В каких случаях индексы нерелевантны? Почему индекс может не использоваться (функция над колонкой, `LIKE '%x'`, низкая селективность, приведение типов)?
- [ ] UNIQUE индекс
- [ ] При создании PK или FK нужен ли дополнительно индекс?
- [ ] Составной индекс. Чем отличается от двух одиночных? Сработает ли индекс по (a, b), если в запросе только одна колонка?
- [ ] Как используются индексы в JOIN?
- [ ] Partial индекс; индекс по выражению
- [ ] Covering index; index only scan
- [ ] Seq scan vs index scan vs bitmap scan — когда что выбирает планировщик?
- [ ] Селективность и кардинальность: что это, как оценить по данным (`pg_stats`: `n_distinct`, `most_common_vals`)? → 🌐 [PG: Statistics Used by the Planner](https://www.postgresql.org/docs/current/planner-stats.html)
- [ ] Почему индекс по булеву полю почти бесполезен? Когда он всё же помогает (сильный перекос данных + partial index `WHERE NOT is_deleted`)? → 🌐 [PG: Partial Indexes](https://www.postgresql.org/docs/current/indexes-partial.html)
- [ ] Порядок колонок в составном индексе: равенство → диапазон → сортировка; когда индекс покрывает `ORDER BY` → 🌐 [PG: Multicolumn Indexes](https://www.postgresql.org/docs/current/indexes-multicolumn.html), [Indexes and ORDER BY](https://www.postgresql.org/docs/current/indexes-ordering.html)
- [ ] Один составной индекс vs несколько одиночных (Bitmap AND): когда что выбрать, trade-off → 🌐 [PG: Combining Multiple Indexes](https://www.postgresql.org/docs/current/indexes-bitmap-scans.html)
- [ ] Цена индекса: медленнее INSERT / UPDATE, место на диске, меньше HOT-обновлений, bloat
- [ ] `EXPLAIN` vs `EXPLAIN ANALYZE`; как читать план: estimated vs actual rows, loops, `Rows Removed by Filter`, `BUFFERS`. Что значит большое расхождение оценок (устаревшая статистика → `ANALYZE`)?
- [ ] Запрос тормозит — что делать по шагам? А если сам запрос уже оптимален?
- [ ] 🌐 `CREATE INDEX CONCURRENTLY` → [PG docs](https://www.postgresql.org/docs/current/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY) ([RU](https://postgrespro.ru/docs/postgresql/current/sql-createindex#SQL-CREATEINDEX-CONCURRENTLY))
- [ ] 🌐 GIN, GiST, BRIN индексы → [PG: Index Types](https://www.postgresql.org/docs/current/indexes-types.html); RUM → [postgrespro/rum](https://github.com/postgrespro/rum)
- [ ] Есть ли индексы только в реляционных БД?

🛠 **Практика: от данных к индексу** (именно на этом срезаются — знают теорию, но в кейсе выбирают не тот индекс)
- [ ] Подними Postgres в Docker, сгенерируй 1–10 млн строк через `generate_series`, сравни планы `EXPLAIN (ANALYZE, BUFFERS)` до и после индекса
- [ ] Кейс: `payments(id, user_id, status, is_test bool, created_at, amount)`, запрос — последние 20 платежей пользователя со `status = 'failed'`. Какой индекс создашь и почему? Почему не три одиночных и не индекс по `is_test`?
- [ ] Медленный запрос: прочитай план, найди проблему (Seq Scan, много `Rows Removed by Filter`, сортировка на диске), предложи индекс и докажи эффект новым планом
- [ ] Для каждого созданного индекса проговори: какие запросы он ускоряет, какую селективность использует, что замедляет
- 🌐 [Use The Index, Luke](https://use-the-index-luke.com/) — бесплатная книга про индексы с точки зрения разработчика (EN)

### 4.7 Транзакции и блокировки
📖 [GI · cache_and_db → «дедлоки»](https://github.com/goavengers/go-interview/blob/master/docs/cache_and_db/README.md) · 🌐 [PG: Concurrency Control](https://www.postgresql.org/docs/current/mvcc.html) · 🌐 [Изоляция транзакций (RU)](https://postgrespro.ru/docs/postgresql/current/transaction-iso) · 🌐 [PG: Explicit Locking](https://www.postgresql.org/docs/current/explicit-locking.html)

- [ ] Что такое транзакция? Основные операции (`BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`)
- [ ] Создаётся ли транзакция, если выполнить команду без явной транзакции?
- [ ] ACID. 🌐 Как обеспечивается Durability? → [PG: WAL](https://www.postgresql.org/docs/current/wal-intro.html)
- [ ] Уровни изоляции транзакций
- [ ] Феномены: dirty read, non-repeatable read, phantom read, lost update, serialization anomaly — на каких уровнях возможны?
- [ ] 🌐 MVCC в PostgreSQL; зачем нужен `VACUUM`? → [PG: Routine Vacuuming](https://www.postgresql.org/docs/current/routine-vacuuming.html) ([RU](https://postgrespro.ru/docs/postgresql/current/routine-vacuuming))
- [ ] ⭐ Как PostgreSQL реализует уровни изоляции (снимки, SSI)?
- [ ] Блокировки таблиц, row-level locking, lock modes
- [ ] 🌐 Как прочитать строки и не заблокироваться на залоченных? → [SELECT: Locking Clause](https://www.postgresql.org/docs/current/sql-select.html#SQL-FOR-UPDATE-SHARE) (`SKIP LOCKED`)
- [ ] `SELECT ... FOR UPDATE`; оптимистичные vs пессимистичные блокировки
- [ ] Lost update: как защититься (FOR UPDATE, колонка `version`, атомарный `UPDATE ... SET x = x + 1`)?
- [ ] Чем опасны длинные транзакции?
- [ ] ⭐ Advisory locks
- [ ] Deadlock в БД: причины, как избежать
- [ ] Распределённые транзакции: 2PC vs 3PC; Saga
- [ ] Каждую аномалию покажи на сценарии с двумя параллельными транзакциями (например, два перевода с одного счёта) и назови уровень изоляции, на котором она исчезает
- [ ] Финтех-кейс: перевод денег между счетами без двойного списания и lost update — `SELECT ... FOR UPDATE` с фиксированным порядком блокировок (против дедлоков), уровень изоляции, idempotency key, журнал проводок (ledger)

### 4.8 ⭐ 🌐 PostgreSQL изнутри
📖 🌐 [Е. Рогов «PostgreSQL 18 изнутри»](https://postgrespro.ru/education/books/internals) (бесплатный PDF, RU) · 🌐 [The Internals of PostgreSQL](https://www.interdb.jp/pg/)

- [ ] Архитектура: процессы (postmaster, backend на соединение, фоновые процессы), shared buffers
- [ ] Как хранится версия строки: `xmin` / `xmax`, видимость, снимки
- [ ] WAL и checkpoint
- [ ] Autovacuum: когда запускается, что если не успевает; bloat; transaction ID wraparound
- [ ] HOT-обновления, TOAST
- [ ] Планировщик: статистика (`ANALYZE`), nested loop vs hash join vs merge join
- [ ] Почему соединение с PG дорогое? PgBouncer: зачем, режимы session / transaction / statement

### 4.9 Масштабирование БД
📖 [GI · cache_and_db](https://github.com/goavengers/go-interview/blob/master/docs/cache_and_db/README.md) · 🌐 PG: [Streaming Replication](https://www.postgresql.org/docs/current/warm-standby.html#STREAMING-REPLICATION), [Logical Replication](https://www.postgresql.org/docs/current/logical-replication.html), [Partitioning](https://www.postgresql.org/docs/current/ddl-partitioning.html)

- [ ] Horizontal vs vertical scaling
- [ ] Как масштабировать чтение и как — запись?
- [ ] Что такое репликация? Sync vs async; master-slave, multi-leader, leaderless (кворумы `R + W > N`)
- [ ] Логическая vs физическая репликация
- [ ] Лаг репликации: как обеспечить read-your-writes при чтении с реплик?
- [ ] ⭐ Failover: как происходит переключение на реплику?
- [ ] Что такое partitioning? Требования к ключу партиционирования
- [ ] Что такое sharding? Подходы: range, hash, consistent hashing; решардинг
- [ ] CAP / PACELC

### 4.10 Go и БД
📖 [GI · podolsky #16](https://github.com/goavengers/go-interview/blob/master/docs/podolsky/README.md)

- [ ] `database/sql`: пул соединений и его настройки
- [ ] Типичные утечки (незакрытые `rows` и т.п.)
- [ ] N+1, SQL-инъекции, prepared statements
- [ ] Есть ли в Go хороший ORM? sqlx, pgx, gorm, sqlc — плюсы и минусы
- [ ] Транзакции в Go: `defer tx.Rollback`, как прокинуть транзакцию через слои
- [ ] Retry при сбоях БД: какие ошибки можно повторять, а какие нет?
- [ ] Миграции (golang-migrate, goose); миграции без даунтайма (expand / contract, новая колонка `NOT NULL`, индекс на живой таблице)

🛠 P: ch-13 · [P · packages](https://github.com/RezaSi/go-interview-practice/tree/main/packages) (gorm, mongodb)

### 4.11 🌐 NoSQL и аналитические хранилища
📖 🌐 [system-design-primer](https://github.com/donnemartin/system-design-primer) (раздел про БД) · 🌐 [DDIA](https://dataintensive.net/) (гл. 3) · 🌐 [TimescaleDB: hypertables](https://www.tigerdata.com/docs/learn/hypertables/understand-hypertables)

- [ ] Типы NoSQL: key-value, document, wide-column, graph, time-series, search
- [ ] SQL vs NoSQL: как выбирать?
- [ ] B-tree vs LSM-tree: как устроены, где что используется?
- [ ] OLTP vs OLAP; колоночное хранение; почему ClickHouse быстрый для аналитики?
- [ ] Time-series БД; что такое hypertable (TimescaleDB)?
- [ ] ⭐ MongoDB: документная модель, индексы, replica set
- [ ] ⭐ Cassandra / ScyllaDB: partition key, clustering key, tunable consistency
- [ ] ⭐ Elasticsearch: инвертированный индекс
- [ ] Object storage (S3): когда хранить файлы там, а не в БД?

### 4.12 Кэширование и Redis
📖 🌐 Redis: [data types](https://redis.io/docs/latest/develop/data-types/), [persistence](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/), [eviction](https://redis.io/docs/latest/develop/reference/eviction/)

- [ ] Стратегии кэширования: cache-aside, write-through, write-back; инвалидация; TTL с jitter
- [ ] Консистентность кэша и БД: в каком порядке обновлять и инвалидировать?
- [ ] Cache stampede: что это и как защититься?
- [ ] Redis: структуры данных, persistence (RDB / AOF), eviction-политики, почему однопоточный Redis быстрый?
- [ ] Горячие ключи и большие ключи — чем опасны?
- [ ] ⭐ Redis Sentinel vs Redis Cluster
- [ ] ⭐ Pub/Sub и Streams в Redis
- [ ] ⭐ 🌐 Распределённая блокировка на Redis — что может пойти не так? → [Redis: Distributed Locks](https://redis.io/docs/latest/develop/clients/patterns/distributed-locks/), [Kleppmann: How to do distributed locking](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html)

🛠 Кэш с TTL · Singleflight · P: ch-28

### 4.13 Брокеры сообщений
📖 🌐 [Kafka Docs: Design](https://kafka.apache.org/43/design/design/) · 🌐 [Kafka: The Definitive Guide](https://www.confluent.io/resources/ebook/kafka-the-definitive-guide/) (бесплатно после регистрации) · 🌐 [RabbitMQ: AMQP 0-9-1 Model](https://www.rabbitmq.com/tutorials/amqp-concepts)

- [ ] Что такое message broker и message queue?
- [ ] Publisher, consumer; механизм pub-sub
- [ ] Плюсы и минусы брокера в сравнении с HTTP. Можно ли любой HTTP-интерфейс заменить брокером? Почему?
- [ ] Push vs pull
- [ ] Что означает broker durability?
- [ ] Гарантии доставки: at-most-once, at-least-once, exactly-once; идемпотентный консьюмер, inbox-таблица для дедупликации
- [ ] Kafka: топик, партиция, offset, consumer group, ребалансировка
- [ ] 🌐 Kafka: репликация, leader, ISR, `acks=0/1/all`, `min.insync.replicas`
- [ ] 🌐 Kafka: идемпотентный продюсер, транзакции, exactly-once semantics
- [ ] Коммит offset: авто vs ручной; что будет при падении консьюмера до и после коммита?
- [ ] Consumer lag: что это, как мониторить?
- [ ] 🌐 Retention и log compaction
- [ ] Ключ партиционирования, горячие партиции; сколько партиций делать?
- [ ] Почему Kafka быстрая (последовательная запись, page cache, zero-copy, батчи)?
- [ ] Как гарантировать, что сообщения прочитаются в том же порядке, в каком записаны?
- [ ] 🌐 RabbitMQ: типы exchange (direct, fanout, topic, headers), ack / nack, requeue
- [ ] 🌐 RabbitMQ: prefetch → [Consumer Prefetch](https://www.rabbitmq.com/docs/consumer-prefetch); lazy queue → [Lazy Queues](https://www.rabbitmq.com/docs/lazy-queues) (устарели с 3.12); ⭐ quorum queues → [Quorum Queues](https://www.rabbitmq.com/docs/quorum-queues)
- [ ] Сравнение двух брокеров (Kafka vs RabbitMQ), плюсы и минусы
- [ ] ⭐ NATS: чем отличается от Kafka и RabbitMQ?
- [ ] Outbox pattern
- [ ] Ретраи, dead letter queue, «ядовитые» сообщения

🛠 Батчер · Pub/Sub

---

<a id="stage-5"></a>
## Этап 5. Архитектура и системы

### 5.1 ООП и принципы проектирования
📖 [GI · README → «шаблоны проектирования», «организация кода»](https://github.com/goavengers/go-interview/blob/master/README.md)

- [ ] Что такое ООП? Принципы: инкапсуляция, наследование, полиморфизм (+ абстракция)
- [ ] Как принципы ООП реализуются в Go без классов и наследования?
- [ ] SOLID: общее определение и каждый принцип с примером на Go
- [ ] DRY, WET, KISS, YAGNI
- [ ] 🌐 Что значит «A little copying is better than a little dependency»? Другие [Go Proverbs](https://go-proverbs.github.io/)
- [ ] ООП vs функциональное программирование
- [ ] 🌐 Компонентно-ориентированное программирование → [Википедия](https://ru.wikipedia.org/wiki/%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)
- [ ] Сцепление (coupling) vs связность (cohesion)
- [ ] Какие паттерны знаешь? Builder, Factory, Singleton, Adapter, Decorator, Strategy, Observer. Какие применял?

### 5.2 Архитектура сервиса

- [ ] Структура Go-проекта; как применять пакеты `internal`
- [ ] Что такое хорошая архитектура своими словами?
- [ ] Что такое чистая архитектура? Какие в ней слои?
- [ ] Как применить инверсию зависимостей в чистой архитектуре?
- [ ] Гексагональная архитектура (ports & adapters)
- [ ] Dependency Injection в Go: любимый способ (вручную, wire, fx)?
- [ ] DDD: bounded context, агрегаты, entity vs value object
- [ ] DDD, BDD, TDD — в чём разница?
- [ ] CQRS; Event Sourcing — когда оправданы?
- [ ] Модульный монолит

### 5.3 Микросервисы
📖 [GI · microservices](https://github.com/goavengers/go-interview/blob/master/docs/microservices/README.md)

- [ ] Что такое микросервисная архитектура?
- [ ] Монолит vs микросервисы: плюсы и минусы
- [ ] Как делить систему на сервисы? Признаки неудачного деления (distributed monolith)
- [ ] Способы общения сервисов: синхронные (REST, gRPC) и асинхронные (брокеры)
- [ ] Паттерн Saga: хореография vs оркестрация
- [ ] API Gateway, service discovery; ⭐ service mesh
- [ ] Как тестировать распределённую систему?

### 5.4 Надёжность и распределённые системы
📖 🌐 [Kleppmann: Distributed Systems (лекции, PDF)](https://www.cl.cam.ac.uk/teaching/2122/ConcDisSys/dist-sys-notes.pdf) · 🌐 [Raft](https://raft.github.io/) · 🌐 [DDIA](https://dataintensive.net/)

- [ ] Как правильно делать ретраи (backoff, jitter)?
- [ ] Circuit breaker — чем отличается от ретраев?
- [ ] Как сделать API идемпотентным?
- [ ] Rate limiting: token bucket, leaky bucket, sliding window
- [ ] Consistent hashing — зачем и как?
- [ ] ⭐ Backpressure, load shedding, bulkhead
- [ ] ⭐ Hedged requests
- [ ] Как распространять дедлайны и отмену между сервисами?
- [ ] 🌐 Модели консистентности: linearizability, sequential, causal, eventual
- [ ] 🌐 Консенсус: Raft (выбор лидера, репликация лога); Paxos на уровне идеи
- [ ] Leader election; задача «ровно на одной реплике»
- [ ] 🌐 Время в распределённых системах: почему нельзя доверять часам? Логические часы Лампорта, векторные часы → [Lamport, 1978 (PDF)](https://lamport.azurewebsites.net/pubs/time-clocks.pdf)
- [ ] Split brain; fencing token
- [ ] Exactly-once — возможно ли? (at-least-once + дедупликация)
- [ ] Генерация уникальных ID: UUID v4 / v7, Snowflake
- [ ] ⭐ Gossip-протоколы, CRDT

🛠 Circuit Breaker · Rate Limiter · Retry · Consistent hashing · P: ch-20, ch-29

### 5.5 System Design
📖 🌐 [system-design-primer](https://github.com/donnemartin/system-design-primer) · 🌐 [ByteByteGo system-design-101](https://github.com/ByteByteGoHq/system-design-101) · [TIH · System design](https://www.techinterviewhandbook.org/system-design/)

Теория:
- [ ] Алгоритм ответа (требования → оценка нагрузки → API → данные → схема → углубление → масштабирование)
- [ ] Back-of-the-envelope оценки; цифры, которые надо помнить (latency numbers, RPS, объёмы)
- [ ] Балансировка: L4 vs L7, алгоритмы, health checks
- [ ] Консистентность: strong, eventual, read-your-writes
- [ ] Горизонтальное масштабирование stateless-сервисов; где хранить состояние
- [ ] 🌐 Как рисовать схемы: нотация [C4](https://c4model.com/) (Авито просит её на секции проектирования)

Типовые задачи (каждую — нарисовать за 45 минут):
- [ ] Сокращатель ссылок
- [ ] Rate limiter
- [ ] Генератор уникальных ID
- [ ] Лента новостей (Instagram)
- [ ] Чат / мессенджер
- [ ] Сервис уведомлений
- [ ] Платёжная система
- [ ] Маркетплейс: корзина и остатки
- [ ] Бронирование (билеты, отели) без двойной продажи
- [ ] Сервис такси / трекинг курьеров на карте (геоиндексы)
- [ ] Счётчик просмотров
- [ ] Распределённый кэш
- [ ] Key-value хранилище
- [ ] Файловое хранилище (S3 / Dropbox)
- [ ] Поисковые подсказки (autocomplete)
- [ ] Распределённый планировщик задач (cron), запуск ровно один раз
- [ ] Система сбора метрик / логов и поиска по логам
- [ ] Распределённая очередь
- [ ] ⭐ Совместный редактор (Google Docs) · разбор
- [ ] Web crawler

---

<a id="stage-6"></a>
## Этап 6. Практика

<a id="s6-1"></a>
### 6.1 🌐 Алгоритмы и структуры данных
📖 🌐 [Яндекс Хендбук «Основы алгоритмов»](https://contest.yandex.ru/tracks/algorithms) · 🌐 [Яндекс «Тренировки по алгоритмам»](https://yandex.ru/yaintern/training/algorithm-training) · 🌐 [NeetCode Roadmap](https://neetcode.io/roadmap) / [NeetCode 150](https://neetcode.io/practice/practice/neetcode150) · 🌐 [LeetCode Top Interview 150](https://leetcode.com/studyplan/top-interview-150/) · [TIH · шпаргалка по темам](https://www.techinterviewhandbook.org/algorithms/study-cheatsheet/) · [TIH · план на 3 месяца](https://www.techinterviewhandbook.org/coding-interview-study-plan/) · [TIH · Grind 75 / Blind 75](https://www.techinterviewhandbook.org/best-practice-questions/)

Теория:
- [ ] Big-O по времени и памяти; амортизированная сложность (почему `append` — O(1) в среднем)
- [ ] Сортировки: quick, merge, heap, counting; стабильность; что использует `slices.Sort` (pdqsort)
- [ ] Структуры данных и сложность операций: массив, связный список, стек, очередь, дек, хеш-таблица, куча, дерево, граф, trie
- [ ] Граничные случаи: пустой ввод, один элемент, дубликаты, отрицательные числа, переполнение (разделы «Corner cases» в TIH)

Паттерны (на каждый решить 3–5 задач):
- [ ] Два указателя · [TIH](https://www.techinterviewhandbook.org/algorithms/array/) · Trapping Rain Water (задача Яндекса)
- [ ] Скользящее окно · [TIH](https://www.techinterviewhandbook.org/algorithms/array/) · Longest Substring
- [ ] Префиксные суммы · [TIH](https://www.techinterviewhandbook.org/algorithms/array/)
- [ ] Строки: анаграммы, палиндромы, подсчёт символов · [TIH](https://www.techinterviewhandbook.org/algorithms/string/)
- [ ] Хеш-таблица: подсчёт, группировка · [TIH](https://www.techinterviewhandbook.org/algorithms/hash-table/) · Two Sum, Group Anagrams
- [ ] Стек; монотонный стек · [TIH](https://www.techinterviewhandbook.org/algorithms/stack/) · Скобочная последовательность
- [ ] Очередь, дек · [TIH](https://www.techinterviewhandbook.org/algorithms/queue/)
- [ ] Бинарный поиск, в т.ч. по ответу · [TIH](https://www.techinterviewhandbook.org/algorithms/sorting-searching/) · Бинарный поиск · P: ch-21
- [ ] Связные списки (fast / slow указатели) · [TIH](https://www.techinterviewhandbook.org/algorithms/linked-list/) · Связный список
- [ ] Деревья: обходы DFS / BFS, BST, высота, LCA · [TIH](https://www.techinterviewhandbook.org/algorithms/tree/)
- [ ] Куча, top-K (`container/heap`) · [TIH](https://www.techinterviewhandbook.org/algorithms/heap/) · Top K
- [ ] Интервалы, sweep line · [TIH](https://www.techinterviewhandbook.org/algorithms/interval/) · Merge Intervals
- [ ] Матрицы: обход, поворот, спираль · [TIH](https://www.techinterviewhandbook.org/algorithms/matrix/)
- [ ] Графы: BFS / DFS, топологическая сортировка, компоненты связности, поиск цикла, Dijkstra · [TIH](https://www.techinterviewhandbook.org/algorithms/graph/) · P: ch-25
- [ ] Рекурсия и backtracking: перестановки, подмножества, комбинации · [TIH](https://www.techinterviewhandbook.org/algorithms/recursion/)
- [ ] Динамическое программирование: 1D, 2D, рюкзак, LIS, LCS · [TIH](https://www.techinterviewhandbook.org/algorithms/dynamic-programming/) · P: ch-24
- [ ] Жадные алгоритмы · P: ch-22
- [ ] Битовые операции · [TIH](https://www.techinterviewhandbook.org/algorithms/binary/)
- [ ] Математика: НОД, простые числа, переполнение · [TIH](https://www.techinterviewhandbook.org/algorithms/math/)
- [ ] ⭐ Trie · [TIH](https://www.techinterviewhandbook.org/algorithms/trie/); Union-Find
- [ ] ⭐ Геометрия · [TIH](https://www.techinterviewhandbook.org/algorithms/geometry/)

Как решать на собесе ([TIH · техники](https://www.techinterviewhandbook.org/coding-interview-techniques/), [TIH · шпаргалка](https://www.techinterviewhandbook.org/coding-interview-cheatsheet/), [TIH · как оценивают](https://www.techinterviewhandbook.org/coding-interview-rubrics/)):
- [ ] Уточнить условие и граничные случаи → озвучить идею и сложность → написать код → прогнать тесты руками
- [ ] Уметь писать без автодополнения и без запуска кода

<a id="s6-2"></a>
### 6.2 Live coding на конкурентность
📖 [GI · popular_tasks](https://github.com/goavengers/go-interview/blob/master/docs/popular_tasks/README.md)

> Цель — не прочитать решение, а **написать с нуля** за 20–30 минут, с тестом и `go test -race`. Каждую задачу реши дважды с перерывом в несколько дней. Фидбек с собесов: «базовое понимание каналов есть, нужно закрепление через практику».

- [ ] Worker pool
- [ ] Fan-in: слить N каналов
- [ ] Pipeline
- [ ] Первый успешный ответ из N реплик
- [ ] Параллельно обойти N URL с лимитом, таймаутом и отменой по первой ошибке · свой errgroup
- [ ] Кэш с TTL
- [ ] Rate limiter
- [ ] Graceful shutdown
- [ ] Батчер
- [ ] Pub/Sub
- [ ] Singleflight
- [ ] Кастомная WaitGroup на семафоре · [GI · popular_tasks #6](https://github.com/goavengers/go-interview/blob/master/docs/popular_tasks/README.md)
- [ ] Параллельно читать из кэша и БД, вернуть первый успешный ответ (Ozon)
- [ ] Краулер: обойти сайт по sitemap через BFS, потом распараллелить с лимитом (Яндекс)
- [ ] In-memory «топ новостей» с конкурентным доступом (VK)
- [ ] Клиентский балансировщик с retry, health-check и circuit breaker (Яндекс)
- [ ] GCE · [Ограничить частоту запросов краулера](https://github.com/loong/go-concurrency-exercises/tree/main/0-limit-crawler)
- [ ] GCE · [Producer-consumer](https://github.com/loong/go-concurrency-exercises/tree/main/1-producer-consumer)
- [ ] GCE · [Гонка в кэше](https://github.com/loong/go-concurrency-exercises/tree/main/2-race-in-cache)
- [ ] GCE · [Лимит времени для бесплатных пользователей](https://github.com/loong/go-concurrency-exercises/tree/main/3-limit-service-time)
- [ ] GCE · [Graceful SIGINT](https://github.com/loong/go-concurrency-exercises/tree/main/4-graceful-sigint)
- [ ] GCE · [Очистка неактивных сессий](https://github.com/loong/go-concurrency-exercises/tree/main/5-session-cleaner)
- [ ] ⭐ Circuit breaker, Retry с jitter

<a id="s6-3"></a>
### 6.3 Code review секция
📖 🌐 [100 Go Mistakes](https://100go.co/)

Уметь найти в чужом коде:
- [ ] Гонку при записи в map / `append` / общую переменную из горутин
- [ ] Утечку горутин (нет выхода, блокировка на канале без читателя)
- [ ] Незакрытые `resp.Body`, `rows`, файлы
- [ ] Проигнорированные ошибки; ошибки без контекста
- [ ] `defer` в цикле
- [ ] Захват переменной цикла (если в `go.mod` версия < 1.22)
- [ ] Типизированный nil в интерфейсе ошибки
- [ ] Копирование структуры с `sync.Mutex` (value receiver)
- [ ] `http.Client` без таймаута; `context.Background` вместо входящего ctx
- [ ] SQL через `fmt.Sprintf` (инъекция)
- [ ] `wg.Add` внутри горутины; канал закрывает не владелец или несколько писателей
- [ ] Паника в горутине без `recover` роняет весь процесс
- [ ] Запись в nil-map
- [ ] Неограниченное число горутин
- [ ] Лишние аллокации: конкатенация в цикле, слайс без предвыделения
- [ ] Читаемость: именование, магические числа, огромные функции, нет тестов
- [ ] Порядок ответа: корректность → конкурентность → ресурсы → ошибки → производительность → читаемость

### 6.4 «Что выведет код»
📖 🌐 [100 Go Mistakes](https://100go.co/) · [GI · popular_tasks #7–10](https://github.com/goavengers/go-interview/blob/master/docs/popular_tasks/README.md)

Типовые темы таких задач — по каждой реши 2–3 примера и объясни вывод:
- [ ] Слайсы: общий базовый массив, `append` внутри функции и внутри `range`, полное выражение среза
- [ ] `defer`: порядок, момент вычисления аргументов, именованный результат, `defer` в цикле
- [ ] nil-интерфейс против интерфейса с nil-указателем; сравнение интерфейсов
- [ ] Замыкания в цикле — с учётом версии в `go.mod`
- [ ] Каналы: чтение из закрытого, запись в nil, `select` с закрытым и nil-каналом
- [ ] Горутины: `main` не ждёт, паника в горутине, `wg.Add` внутри горутины
- [ ] Map: порядок итерации, изменение поля структуры в map, `NaN` как ключ
- [ ] Строки: `len` и `range`, `string(int)`
- [ ] Переполнение целых, размер структуры с padding
- [ ] `recover` во вложенной функции, паника внутри `sync.Once`
- [ ] ⭐ Итераторы (`range` по функции): `break` и итератор, который не проверяет `yield`
### 6.5 Ситуационные задачи

«Что бы вы сделали, если…» — разобрать вслух:
- [ ] Найти и починить race condition в коде
- [ ] Оптимизировать медленный SQL-запрос
- [ ] Спроектировать API для сервиса
- [ ] Спроектировать схему БД под задачу
- [ ] Написать конкурентный обработчик данных
- [ ] Найти утечку памяти в работающем сервисе
- [ ] Реализовать retry-механизм
- [ ] Подобрать индексы под набор запросов и обосновать каждый: селективность, порядок колонок, цена на запись
- [ ] Найти и исправить аномалию в транзакционном коде (перевод денег, списание остатков)

---

<a id="stage-7"></a>
## Этап 7. Перед собеседованием

<a id="s7-1"></a>
### 7.1 Форматы собесов в бигтехе
> По официальным страницам компаний и отчётам кандидатов за 2025–2026. Форматы меняются: перед собесом перечитай страницу компании.

| Компания | Секции | На что обратить внимание |
|---|---|---|
| [Яндекс](https://yandex.ru/jobs/interview/backend) | Go-кодинг (1 ч: язык, горутины, `sync`, каналы) · 2 алгоритмические задачи (easy/medium) · архитектура (если есть опыт highload) · секция про опыт (STAR) | Онлайн-редактор без IDE, ИИ нельзя, код могут не запускать. В архитектуре считают RPS, объёмы, SLA. У кандидатов: краулер sitemap (BFS → распараллелить), лента Instagram ([habr](https://habr.com/ru/articles/1006022/)) |
| [Ozon](https://ozon.tech/career/interview-go/) | Go (runtime, mutex vs каналы, «почему сервис ест много памяти») + обязательный онлайн-кодинг · архитектура на задачах Ozon · в части команд алгоритмы, БД, ОС и сети | Troubleshooting и Linux. У кандидата: «параллельно читать из кэша и БД», SQL, ревью неправильного lock, SD Instagram с расчётом записи на диск ([habr](https://habr.com/ru/articles/926214/)) |
| [Авито](https://career.avito.com/directions/developer/) | Скрининг (алгоритмы, язык, HTTP, SQL, Git, Unix) · программирование (с оценкой big O) · «платформа»: писать и читать код · проектирование (уровень E5+, нотация C4) · soft skills | Git и Unix уже на скрининге; схемы в нотации [C4](https://c4model.com/) |
| [Т-Банк](https://www.tbank.ru/career/it/interview/go/) | Go 90 мин: код-ревью с доработкой, troubleshooting, асинхронность, примитивы · алгоритмы 60 мин: деревья, сортировки, DP · system design 60 мин: API, оценка нагрузки, потоки данных | Есть [открытые критерии SD](https://opensource.tbank.ru/general/career/-/blob/main/interview/sections/system-design-backend.md). У кандидата: SQL с выполнением запросов, SD трекинга курьеров с геоиндексами |
| VK | Скрининг: индексы, шардинг, TCP/UDP, процессы и потоки, безопасность, two-sum · лайвкодинг в своей IDE с тестами (in-memory «топ новостей») | Официального описания нет, по отчёту [кандидата](https://habr.com/ru/articles/1006022/) |
| Wildberries | Теория (SOLID, интерфейсы, сети), код-ревью, поиск гонок и проблем с замыканиями, Kafka (гарантии, consumer group), `sync.Map` | Официального описания нет; по mock-интервью и краудсорсу |
| [SberDevices](https://sberdevices.ru/career/Go/interview/) | Скрининг Go · алгоритмические и Go-задачи · архитектура (блок-схемы) · HR о ценностях | Все секции можно пройти за день |
| [МТС](https://habr.com/ru/companies/ru_mts/articles/909158/) | ~3 задачи до 45 мин: «что выведет», merge каналов, таймауты, параллельный fetch URL с context, код-ревью и рефакторинг | — |
| Касперский | 3 этапа; глубоко про слайсы, интерфейсы, select, каналы | Планка «всё идеально» ([отзыв](https://dreamjob.ru/employers/104814/interviews)) |
| [Amazon](https://www.amazon.jobs/content/en/how-we-hire/sde-ii-interview-prep) (FAANG) | 4 × 55 мин: кодинг, минимум один system design, Leadership Principles по STAR | Кодинг не привязан к языку, behavioral весит больше, чем в RU |
| Плата (финтех) | Техническое: вопросы по Go + задача на горутины · code review (уточняющие вопросы, объяснение решений) · SQL-задача + вопросы по индексам · финал: рассказ об опыте | По фидбеку кандидата (2026): проверяют **применение** знаний БД на рабочем кейсе — составной индекс vs несколько отдельных, селективность, индекс по булеву полю; нормализацию и аномалии; на финале ждут сложный кейс с личным вкладом |

Форматы FAANG и других западных компаний: [TIH · Interview formats](https://www.techinterviewhandbook.org/interview-formats-top-companies/)

Записи реальных собесов на YouTube: [Ozon, скрининг](https://www.youtube.com/watch?v=f5lcPQNNidc) · [Ozon, техническое](https://www.youtube.com/watch?v=-8JlOr3Z0eA) · [Ozon, финал](https://www.youtube.com/watch?v=PZAQTNSG0xg) · [WB, техническое](https://www.youtube.com/watch?v=KJIchjXmXJ8) · [Авито, алгоритмы Middle](https://www.youtube.com/watch?v=RjUClkSm81E) · [ВсеИнструменты, Middle](https://www.youtube.com/watch?v=VD6orbctNgA)

**Что общее почти у всех:**
- [ ] Писать код без IDE, без запуска и без ИИ → тренируйся в простом редакторе (6.1, 6.2)
- [ ] Код-ревью Go-кода (6.3) и задачи на конкурентность (6.2)
- [ ] Troubleshooting: «куда уходит память», «почему тормозит» (3.3, 3.4)
- [ ] SQL вживую, иногда с запуском запросов (4.5)
- [ ] В system design считать нагрузку и мощности: RPS, объёмы, latency numbers (5.5)

<a id="s7-2"></a>
### 7.2 Поведенческие вопросы и секция о проектах
📖 [TIH · Behavioral interview](https://www.techinterviewhandbook.org/behavioral-interview/) · [TIH · 30 частых вопросов](https://www.techinterviewhandbook.org/behavioral-interview-questions/) · [TIH · как оценивают](https://www.techinterviewhandbook.org/behavioral-interview-rubrics/) · [TIH · для Senior](https://www.techinterviewhandbook.org/behavioral-interview-senior-candidates/) · [TIH · самопрезентация](https://www.techinterviewhandbook.org/self-introduction/) · [TIH · вопросы к интервьюеру](https://www.techinterviewhandbook.org/final-questions/)

Подготовить истории по STAR (ситуация → задача → действия → результат):
- [ ] Расскажи о себе (2 минуты)
- [ ] Архитектура последнего проекта: нарисовать, объяснить решения, узкие места, что будет при нагрузке ×10
- [ ] Самый сложный баг или инцидент в проде: как нашёл, как починил, что изменили после
- [ ] Конфликт или несогласие с решением в команде
- [ ] Ошибка или провал и что вынес
- [ ] Инициатива: что улучшил сам, без запроса
- [ ] Трейд-офф: когда осознанно выбрал «хуже, но быстрее»
- [ ] Несогласие с менеджером
- [ ] Жёсткий дедлайн: как успел или что сделал, когда не успевал
- [ ] Самый полезный фидбек, который получал; как реагируешь на критику
- [ ] Что ищешь в следующей роли? Что раздражает в работе?
- [ ] ⭐ Senior: истории про влияние на команду и решения, а не только про технику
- [ ] Почему уходишь / почему к нам
- [ ] Свои вопросы к интервьюеру

**Выбор кейсов для рассказа об опыте.** Простой пример на финале не даёт оценить глубину (реальный фидбек). Подготовь 2–3 **сложных** кейса, где виден твой личный вклад и технические решения:
- [ ] Кейс 1–3: контекст → проблема → какие варианты рассматривал и их trade-off → что выбрал и почему → результат в цифрах (латентность, RPS, деньги, инциденты) → что сделал бы иначе
- [ ] Для каждого кейса будь готов к углублению: «почему не X?», «что было самым сложным?», «как проверяли?»

### 7.3 Финальный прогон
- [ ] Что нового в Go 1.22–1.27 · 🌐 [uproger: Go 1.27 — 20 примеров](https://uproger.com/go-1-27-20-gotovyh-primerov-s-kodom-dlya-prodvinutogo-razrabotchika/)
- [ ] Как проходит собеседование: этапы, что оценивают на live coding
- [ ] Чек-лист подготовки
- [ ] Mock-интервью: минимум одно по алгоритмам, одно по Go и одно по system design

<a id="s7-4"></a>
### 7.4 Резюме, моки, оффер
📖 [TIH · Resume](https://www.techinterviewhandbook.org/resume/) · [TIH · Mock interviews](https://www.techinterviewhandbook.org/mock-interviews/) · [TIH · Negotiation](https://www.techinterviewhandbook.org/negotiation/) · [TIH · правила переговоров](https://www.techinterviewhandbook.org/negotiation-rules/) · [TIH · Compensation](https://www.techinterviewhandbook.org/understanding-compensation/) · [TIH · выбор компании](https://www.techinterviewhandbook.org/choosing-between-companies/) · [TIH · уровни](https://www.techinterviewhandbook.org/engineering-levels/)

- [ ] Резюме: проходит ATS, результаты в цифрах, ключевые слова из вакансии
- [ ] Самопрезентация на 1–2 минуты (elevator pitch)
- [ ] Где пройти mock-интервью
- [ ] Чего ждут от Middle и от Senior: на какой уровень ты претендуешь?
- [ ] Как сравнивать офферы и компании
- [ ] Переговоры о зарплате: правила, когда называть цифру, как торговаться
- [ ] Из чего состоит компенсация (оклад, премия, акции, льготы)

---

<a id="resources"></a>
## Ресурсы

**Go**
- [Go Spec](https://go.dev/ref/spec) · [Effective Go](https://go.dev/doc/effective_go) · [Go Memory Model](https://go.dev/ref/mem) · [GC Guide](https://go.dev/doc/gc-guide) · [Diagnostics](https://go.dev/doc/diagnostics)
- [100 Go Mistakes](https://100go.co/) · [Ardan Labs: Scheduling in Go](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part1.html) · [Russ Cox: Interfaces](https://research.swtch.com/interfaces) · [Go Blog: Slices](https://go.dev/blog/slices-intro)

**ОС, сети, Linux**
- [OSTEP](https://pages.cs.wisc.edu/~remzi/OSTEP/) · [High Performance Browser Networking](https://hpbn.co/) · [what-happens-when](https://github.com/alex/what-happens-when) · [Brendan Gregg: Linux Performance](https://www.brendangregg.com/linuxperf.html)

**Базы данных**
- [PostgreSQL docs](https://www.postgresql.org/docs/current/) ([RU](https://postgrespro.ru/docs/postgresql/current/)) · [Рогов «PostgreSQL 18 изнутри»](https://postgrespro.ru/education/books/internals) · [The Internals of PostgreSQL](https://www.interdb.jp/pg/) · [Database Internals (А. Петров)](https://www.databass.dev/) — книгу советует Т-Банк
- Тренажёры SQL: [pgexercises.com](https://pgexercises.com/) · [sql-ex.ru](https://sql-ex.ru/)

**Брокеры и кэш**
- [Kafka Design](https://kafka.apache.org/43/design/design/) · [Kafka: The Definitive Guide](https://www.confluent.io/resources/ebook/kafka-the-definitive-guide/) · [RabbitMQ docs](https://www.rabbitmq.com/docs) · [Redis docs](https://redis.io/docs/latest/)

**Распределённые системы и system design**
- [DDIA (Клеппман)](https://dataintensive.net/) · [Kleppmann: лекции](https://www.cl.cam.ac.uk/teaching/2122/ConcDisSys/dist-sys-notes.pdf) · [Raft](https://raft.github.io/) · [system-design-primer](https://github.com/donnemartin/system-design-primer) · [ByteByteGo system-design-101](https://github.com/ByteByteGoHq/system-design-101) · [Google SRE book](https://sre.google/sre-book/service-level-objectives/)

**Алгоритмы**
- [Яндекс Хендбук](https://contest.yandex.ru/tracks/algorithms) · [Яндекс Тренировки](https://yandex.ru/yaintern/training/algorithm-training) · [NeetCode](https://neetcode.io/roadmap) · [LeetCode Top Interview 150](https://leetcode.com/studyplan/top-interview-150/)

**Практика и банки вопросов**
- [go-interview-practice](https://github.com/RezaSi/go-interview-practice) · [go-concurrency-exercises](https://github.com/loong/go-concurrency-exercises) · [Tech Interview Handbook](https://www.techinterviewhandbook.org/) · [goavengers/go-interview](https://github.com/goavengers/go-interview)
- [shadowhint: 1300+ вопросов с Go-собесов](https://shadowhint.com/questions/technology/golang-razrabotchik) · [Go Proverbs](https://go-proverbs.github.io/)

**Прочее**
- [Pro Git (RU)](https://git-scm.com/book/ru/v2) · [OWASP Top 10](https://top10.owasp.org/2025/) · [Google API design guide](https://docs.cloud.google.com/apis/design) · [Kubernetes docs](https://kubernetes.io/ru/docs/concepts/overview/) · [Docker docs](https://docs.docker.com/get-started/docker-overview/)
