# Go Backend Interview Roadmap

Единый список тем и вопросов, собранный из `Wolves`, `sobesrazborgoogle`, `go-interview` и `go-interview-practice`, дополненный темами, которые спрашивают в бигтехе. Дубли объединены. Ответов здесь нет: сначала отвечаешь сам, потом сверяешься с источником.

**Обозначения**
- `[ ]` → `[x]` — когда можешь ответить вслух, без подсказок
- ⭐ — Senior / углублённый уровень, на первом проходе можно пропустить
- 🌐 — в локальных файлах ответа нет, ссылка на внешний источник в строке или в 📖
- 📖 — где искать ответы · 🛠 — практика по теме

**Источники**
- **S** — `sources/sobesrazborgoogle/README.md` — основной источник ответов
- **GI** — `sources/go-interview/`
- **P** — `sources/go-interview-practice/challenge-N` — задачи с тестами
- Внешние ссылки проверены на доступность (сентябрь 2026); сводный список — в разделе «Ресурсы» в конце

**Как проходить:** тема → ответить на вопросы сам → сверить → практика 🛠 → следующая тема. Этапы 1–2 по порядку, дальше можно параллелить. Алгоритмы (6.1) решай параллельно с теорией с первого дня, по 1–2 задачи в день.

---

## Этап 1. Язык Go

### 1.1 Базовые типы и синтаксис
📖 [S · Основы](sources/sobesrazborgoogle/README.md#основы-go-вопросы-на-собеседовании-с-ответами) · [S · Топ-20](sources/sobesrazborgoogle/README.md#топ-20-вопросов-на-собеседовании-go) · [GI · README](sources/go-interview/README.md) · [GI · podolsky](sources/go-interview/docs/podolsky/README.md) · 🌐 [Go Spec](https://go.dev/ref/spec)

- [ ] Чем Go отличается от других языков (Java, Python)? Почему его выбирают для backend?
- [ ] Технологические преимущества и недостатки Go
- [ ] Go — императивный или декларативный? В чём разница?
- [ ] Какие типы есть в Go (целые, float, complex, string, bool, составные)?
- [ ] Что такое zero value? Нулевые значения всех типов
- [ ] `var x int`, `x := 0`, `new(int)` — в чём разница?
- [ ] `new` vs `make`
- [ ] Отличия `int`, `int32`, `int64`. Чем `int` отличается от `uint`? От чего зависит размер `int`?
- [ ] Сколько памяти занимают `int32`/`int64`, их предельные значения? Что при переполнении?
- [ ] Что будет при делении int на 0 и float на 0?
- [ ] Преобразования между строками и числами (`strconv`). Можно ли сделать `string(int)` и `int(string)`?
- [ ] Константы: можно ли изменить? Типизированные vs нетипизированные
- [ ] Что такое `iota`? Как сделать enum?
- [ ] Shadowing переменных — что это и чем опасно?
- [ ] Модификаторы доступа (экспортируемые имена)
- [ ] `type A B` vs `type A = B`
- [ ] Что делает `_` (blank identifier)?
- [ ] Какие циклы есть в Go? Как завершить `for` без условия? `break`/`continue` с меткой, `goto`
- [ ] Что изменилось в циклах `for` в Go 1.22 (переменная цикла, `range int`)?
- [ ] Как устроен `switch` (fallthrough, switch без выражения)?
- [ ] Порядок выполнения логических операций, short-circuit. `true && !false`? `(true && false) || (false && true) || !(false && false)`?
- [ ] Пакет `fmt`: `Println`, `Printf`, `Sprintf`, `Scan`; основные verbs (`%v`, `%+v`, `%T`)
- [ ] Пакеты: как создавать и импортировать? Порядок инициализации пакета

🛠 [S · вывод](sources/sobesrazborgoogle/README.md#что-выведет-этот-код--25-каверзных-задач-по-go-с-собеседований) #20 · P: ch-1, ch-18

### 1.2 Строки, руны, байты
📖 [S · Слайсы, map и строки → «Строки»](sources/sobesrazborgoogle/README.md#слайсы-map-и-строки-в-go-устройство-и-вопросы-на-собеседовании) · [GI · golang #1–2](sources/go-interview/docs/golang/README.md)

- [ ] Как устроена строка? Почему immutable, почему нельзя `s[0] = 'a'`?
- [ ] Что такое `rune` и `byte`?
- [ ] Как в UTF-8 кодируется, сколькими байтами описан конкретный символ?
- [ ] Длина строки в байтах и в символах: что вернёт `len("привет")`? `utf8.RuneCountInString`
- [ ] Как работает `range` по строке? Чем отличается от итерации по индексу?
- [ ] Что происходит при конкатенации? Как эффективно склеивать много строк (`strings.Builder`, `bytes.Buffer`, `strings.Join`)?
- [ ] Конвертация `string ↔ []byte` — всегда ли копирование?
- [ ] Пакет `strings`: основные функции; новое в `strings`/`bytes`

🛠 S · вывод #21 · [S · RLE-сжатие](sources/sobesrazborgoogle/README.md#rle-сжатие-строки) · P: ch-2, ch-17, ch-23, ch-26

### 1.3 Массивы и слайсы
📖 [S · Слайсы, map и строки → «Слайсы»](sources/sobesrazborgoogle/README.md#слайсы-map-и-строки-в-go-устройство-и-вопросы-на-собеседовании) · [GI · README](sources/go-interview/README.md) · 🌐 [Go Blog: Slices internals](https://go.dev/blog/slices-intro)

- [ ] Массив vs слайс. Массив — значение: что из этого следует?
- [ ] Как устроен слайс (ptr, len, cap)? Сколько весит заголовок слайса?
- [ ] Способы создать слайс. nil-слайс vs пустой слайс; можно ли `append` в nil? Как проверить на пустоту?
- [ ] Как работает `append` и рост capacity (старая и новая формула)? Можно ли `append` к массиву? Напиши свой `append`
- [ ] Общий базовый массив: когда изменение одного слайса видно в другом?
- [ ] Слайс передан в функцию: изменится ли он снаружи при изменении элемента? А при `append`?
- [ ] Реслайсинг `s[a:b]`; полное выражение `s[a:b:c]` — зачем?
- [ ] Как скопировать слайс (`copy`, трюк с `append`)? Как слить два слайса?
- [ ] Удаление элемента с сохранением порядка и без
- [ ] Big-O всех операций со слайсом
- [ ] Утечка памяти через подслайс — как избежать?
- [ ] Пакет `slices` (Go 1.21+)
- [ ] Как отсортировать слайс структур по полю (`sort.Slice`, `slices.SortFunc`)?

🛠 S · вывод #1–5, #22, #23, ⭐#35, ⭐#36 · [S · Two Sum](sources/sobesrazborgoogle/README.md#two-sum--найти-два-числа-с-заданной-суммой) · [S · Пересечение слайсов](sources/sobesrazborgoogle/README.md#пересечение-двух-слайсов) · P: ch-19

### 1.4 Map и хеш-таблицы
📖 [S · Слайсы, map и строки → «Map»](sources/sobesrazborgoogle/README.md#слайсы-map-и-строки-в-go-устройство-и-вопросы-на-собеседовании) · [S · Продвинутый #6](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior) · [GI · podolsky #6–7](sources/go-interview/docs/podolsky/README.md)

- [ ] Как работает хеш-таблица? Что такое хеш-функция?
- [ ] Методы разрешения коллизий (цепочки, открытая адресация)
- [ ] Как устроена map в Go под капотом (классическая: `hmap`, бакеты)? Сколько элементов в бакете?
- [ ] Что такое эвакуация, когда она происходит и как её избежать?
- [ ] ⭐ Map на Swiss Tables (Go 1.24+): чем отличается от старой реализации?
- [ ] Как происходит поиск по ключу?
- [ ] Что вернётся по несуществующему ключу? Как проверить наличие ключа?
- [ ] Чтение и запись в nil-map
- [ ] Что может быть ключом map?
- [ ] Почему порядок итерации по map случайный?
- [ ] Почему нельзя взять адрес элемента `&m[k]`? Как изменить поле структуры, лежащей в map?
- [ ] Освобождает ли `delete` память? Как избежать утечек памяти в слайсах и map?
- [ ] Big-O операций с map
- [ ] Сколько весят слайс, map, пустая строка, int?

🛠 S · вывод #25, ⭐#26 · [S · Group Anagrams](sources/sobesrazborgoogle/README.md#group-anagrams--группировка-анаграмм) · [S · Top K](sources/sobesrazborgoogle/README.md#top-k-frequent--k-самых-частых-элементов) · P: ch-6

### 1.5 Функции, методы, замыкания, defer
📖 [S · Основы #6, #10, #11, #13](sources/sobesrazborgoogle/README.md#основы-go-вопросы-на-собеседовании-с-ответами) · [S · Интерфейсы #4, #11, #13](sources/sobesrazborgoogle/README.md#интерфейсы-структуры-и-методы-в-go)

- [ ] Зачем нужны функции? Функции как значения (first-class)
- [ ] Чем полезны анонимные и вариативные функции?
- [ ] Замыкание: что это, примеры, где полезно
- [ ] Рекурсия: примеры, какие проблемы (глубина стека, производительность)?
- [ ] Передача аргументов: по значению или по ссылке? Какие типы ведут себя как ссылки?
- [ ] Функция vs метод. Как создать свой метод? Можно ли объявить метод на типе из другого пакета?
- [ ] Value receiver vs pointer receiver — когда что? Method set
- [ ] Функция `init()`: зачем нужна, порядок вызова
- [ ] `defer`: зачем, порядок вызова, когда вычисляются аргументы
- [ ] Захват значений переменных в `defer`; `defer` и именованный результат
- [ ] Как вернуть ошибку изнутри `defer` (не просто залогировать)?
- [ ] ⭐ Функциональные опции (functional options)
- [ ] Напиши `swap(&x, &y)`

🛠 S · вывод #6–8, #12, #16, ⭐#28, ⭐#34

### 1.6 Структуры, интерфейсы, указатели
📖 [S · Интерфейсы, структуры и методы](sources/sobesrazborgoogle/README.md#интерфейсы-структуры-и-методы-в-go) · [GI · README](sources/go-interview/README.md) · [GI · podolsky #2–3, #13, #25](sources/go-interview/docs/podolsky/README.md) · 🌐 [Russ Cox: Go Data Structures: Interfaces](https://research.swtch.com/interfaces)

- [ ] Что такое структура, зачем? Теги структур
- [ ] Можно ли сравнивать структуры? Пустая структура `struct{}` — зачем?
- [ ] Выравнивание полей (alignment/padding), размер структуры
- [ ] Что такое указатели? Когда их использовать?
- [ ] Что такое интерфейс? Утиная типизация; чем отличается от интерфейсов в Java/PHP?
- [ ] Неявная реализация интерфейсов — плюсы и минусы. Как заставить компилятор проверить, что тип реализует интерфейс?
- [ ] Интерфейс как структура: `iface`, `eface`, `itab`
- [ ] Пустой интерфейс, `any` — когда использовать?
- [ ] nil-интерфейс ≠ интерфейс с nil-значением. Как вызов метода на интерфейсе, не равном nil, может упасть с nil pointer dereference?
- [ ] Сравнение интерфейсов
- [ ] Type assertion и `switch v := x.(type)`: способы применения
- [ ] Где объявлять интерфейс: на стороне потребителя или реализации? Почему?
- [ ] Embedding — это наследование? Почему нет?
- [ ] Почему нельзя копировать структуру с `sync.Mutex` внутри? Как это ловит `go vet`?
- [ ] ⭐ Когда интерфейс вызывает аллокацию?
- [ ] Сериализация: что это, зачем; JSON-теги, неэкспортируемые поля
- [ ] Реализуй интерфейс площади для `Circle` и `Square`

🛠 S · вывод #9–12, #24, ⭐#32 · P: ch-3, ch-10

### 1.7 Ошибки, panic, recover
📖 [S · Обработка ошибок](sources/sobesrazborgoogle/README.md#обработка-ошибок-panic-и-recover-в-go) · [GI · podolsky #14](sources/go-interview/docs/podolsky/README.md)

- [ ] Что такое `error`? Как правильно обрабатывать ошибки?
- [ ] Sentinel errors, кастомные типы ошибок, обёртки — когда что?
- [ ] Зачем врапать ошибки? Способы врапинга (`%w`, свой тип с `Unwrap`)
- [ ] `errors.Is` vs `errors.As` vs `==`; `errors.AsType`
- [ ] Несколько ошибок сразу (`errors.Join`)
- [ ] Recoverable vs fatal ошибки: как это сделано в пакете `net` и как делать в современном Go?
- [ ] Что такое panic? Когда её использовать? Что будет при `panic(nil)`?
- [ ] Как работает `recover`? Поймает ли он панику из другой горутины? Что нельзя поймать?
- [ ] Порядок выполнения при панике
- [ ] Ошибка в `defer f.Close()` — теряем? Как не потерять?

🛠 S · вывод #13, #14, ⭐#39, ⭐#40 · P: ch-7, ch-12

### 1.8 Дженерики
📖 [S · Дженерики](sources/sobesrazborgoogle/README.md#дженерики-в-go-118--127-вопросы-и-ответы) · [GI · podolsky #26](sources/go-interview/docs/podolsky/README.md)

- [ ] Какие средства обобщённого программирования есть в Go?
- [ ] Синтаксис и constraints; `comparable`, `~T`, union-типы
- [ ] Как реализованы дженерики (GC shape stenciling)? Есть ли оверхед?
- [ ] Дженерики или интерфейсы — когда что?
- [ ] Что нельзя делать с дженериками?
- [ ] Инференс типов
- [ ] ⭐ Итераторы range-over-func (Go 1.23), `iter.Pull`
- [ ] ⭐ Параметризованные алиасы (1.24), самоссылающиеся ограничения (1.26), generic-методы (1.27)

🛠 [S · Senior-вывод](sources/sobesrazborgoogle/README.md#что-выведет-этот-код--senior-уровень-ещё-15-задач) ⭐#29, ⭐#37, ⭐#38 · [S · LRU Cache](sources/sobesrazborgoogle/README.md#lru-cache-на-go-generics--containerlist) · P: ch-27

### 1.9 Стандартная библиотека и тулинг
📖 🌐 [Effective Go](https://go.dev/doc/effective_go) · 🌐 [pkg.go.dev/std](https://pkg.go.dev/std) · 🌐 [100 Go Mistakes](https://100go.co/)

- [ ] `io.Reader` / `io.Writer`: зачем, как композируются (`io.Copy`, `io.TeeReader`, `io.MultiWriter`, `io.LimitReader`)?
- [ ] `bufio`: когда нужен и почему быстрее?
- [ ] Работа с файлами: `os.Open` vs `os.ReadFile`, закрытие, чтение большого файла построчно
- [ ] `time`: `Duration`, таймзоны, `time.After` в цикле, зачем `Ticker.Stop()`
- [ ] `encoding/json`: теги, `omitempty`, `json.RawMessage`, потоковый `json.Decoder`; почему медленный и чем заменить?
- [ ] `net/http` клиент: почему клиент надо переиспользовать, зачем закрывать и дочитывать `resp.Body`, пул соединений в `Transport`
- [ ] `container/heap`, `container/list` — когда пригодятся?
- [ ] `golang.org/x/sync`: `errgroup`, `semaphore`, `singleflight`
- [ ] `go vet`, `staticcheck`, `golangci-lint`, `gofmt` / `goimports`
- [ ] `//go:embed`, build tags (`//go:build`), `go generate`
- [ ] Кросс-компиляция (`GOOS`/`GOARCH`), `CGO_ENABLED=0`

---

## Этап 2. Конкурентность и runtime

### 2.1 Потоки, горутины, планировщик
> Ментор Wolves про планировщик: «буду очень подробно спрашивать».

📖 [S · Горутины и каналы #1–2, #15](sources/sobesrazborgoogle/README.md#горутины-и-каналы-вопросы-на-собеседовании-по-конкурентности-в-go) · [S · Runtime → «Планировщик»](sources/sobesrazborgoogle/README.md#runtime-go-планировщик-стек-escape-analysis-и-сборщик-мусора) · [S · Продвинутый #4](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior) · 🌐 Ardan Labs: [Scheduling in Go I](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part1.html), [II](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part2.html)

- [ ] Что такое процесс и поток ОС?
- [ ] Что такое системный вызов? Сетевой вызов?
- [ ] Конкурентность vs параллелизм
- [ ] Что такое горутина? Горутина vs поток ОС. Сколько памяти занимает, как растёт стек?
- [ ] Типы многозадачности: вытесняющая и кооперативная. Какая в Go сейчас и какая была до 1.14?
- [ ] Переключение контекста: что происходит, почему у потоков дороже, чем у горутин?
- [ ] Модель G-M-P: что такое G, M, P; локальная и глобальная очереди, `runnext`
- [ ] Work stealing
- [ ] Что происходит при блокирующем системном вызове (hand off P)? Что такое netpoller?
- [ ] Вытеснение (preemption): кооперативное и асинхронное (sysmon, `SIGURG`)
- [ ] Какие бывают состояния у горутин?
- [ ] `GOMAXPROCS`; поведение в контейнерах (Go 1.25)
- [ ] `runtime.Gosched()`, `runtime.Goexit()`, `LockOSThread`
- [ ] ⭐ Что делает `sysmon`?

### 2.2 Каналы и select
📖 [S · Горутины и каналы](sources/sobesrazborgoogle/README.md#горутины-и-каналы-вопросы-на-собеседовании-по-конкурентности-в-go) · [S · Продвинутый #1–3](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior) · [GI · golang #8–10, #22](sources/go-interview/docs/golang/README.md)

- [ ] Что такое канал и зачем нужен? Как устроен (`hchan`)?
- [ ] Буферизированный vs небуферизированный канал. Как создать, закрыть, задать направление?
- [ ] Чтение / запись / закрытие для nil-канала, открытого и закрытого — что будет в каждом случае?
- [ ] Кто должен закрывать канал? Что будет, если закрыть закрытый канал?
- [ ] Что будет, если отправить в канал, у которого нет читателей?
- [ ] Как работает `select`? Порядок выбора, `default`, nil-каналы в `select`
- [ ] Как сделать таймаут на операцию (`select` + `time.After` / `context`)?
- [ ] Что такое deadlock? Когда рантайм его ловит?
- [ ] Goroutine leak: что это, как найти и предотвратить?
- [ ] Как дождаться завершения горутин? Как остановить горутину извне?
- [ ] Как ограничить число одновременных горутин?
- [ ] Паттерны: generator, fan-in, fan-out, pipeline, worker pool, semaphore, pub/sub, or-done, tee
- [ ] Каналы или мьютексы — когда что?
- [ ] Можно ли реализовать `sync.Mutex` и `sync.WaitGroup` на каналах? Как?
- [ ] Напиши свой `Sleep` через `time.After`
- [ ] ⭐ Как работает `select` внутри? Что изменилось в таймерах в Go 1.23?

🛠 S · вывод #15, #17–19, ⭐#30, ⭐#33 · [S · Worker Pool](sources/sobesrazborgoogle/README.md#worker-pool-на-go) · [S · Fan-in](sources/sobesrazborgoogle/README.md#fan-in-слить-n-каналов-в-один) · [S · Pipeline](sources/sobesrazborgoogle/README.md#pipeline-конвейер-на-каналах) · [S · Первый ответ из N](sources/sobesrazborgoogle/README.md#первый-успешный-ответ-из-n-реплик-с-таймаутом) · [GI · popular_tasks #2–6](sources/go-interview/docs/popular_tasks/README.md) · P: ch-4, ch-8, ch-11

### 2.3 sync, atomic, модель памяти
📖 [S · sync, atomic и модель памяти](sources/sobesrazborgoogle/README.md#sync-atomic-и-модель-памяти-go) · [S · Слайсы, map → #15, #19](sources/sobesrazborgoogle/README.md#слайсы-map-и-строки-в-go-устройство-и-вопросы-на-собеседовании) · [GI · podolsky #18–20](sources/go-interview/docs/podolsky/README.md) · 🌐 [The Go Memory Model](https://go.dev/ref/mem)

- [ ] Что такое race condition? Чем отличается от data race? Как найти (`-race`)?
- [ ] Какие способы синхронизации есть в Go?
- [ ] `sync.Mutex`: как устроен? Какие типы мьютексов есть в stdlib?
- [ ] ⭐ Нормальный режим и режим голодания (starvation mode) у `sync.Mutex`
- [ ] `Mutex` vs `RWMutex`; когда `RWMutex` выгоден?
- [ ] Особенности работы с map в горутинах: что будет при конкурентной записи, как защититься?
- [ ] `sync.Map`: как устроена, какие недостатки? Что лучше: map + mutex или `sync.Map`?
- [ ] `sync.WaitGroup` (и `wg.Go`, Go 1.25); `sync.Once`, `OnceFunc`, `OnceValue`
- [ ] `sync.Cond` — зачем, если есть каналы?
- [ ] `sync.Pool`
- [ ] `sync/atomic`: что умеет, когда лучше мьютекса?
- [ ] Модель памяти Go, happens-before
- [ ] Можно ли использовать один буфер `[]byte` в нескольких горутинах?
- [ ] Можно ли захватить мьютекс с таймаутом?
- [ ] Как тестировать конкурентный код без `time.Sleep`?
- [ ] ⭐ False sharing
- [ ] ⭐ Lock-free структуры данных, CAS, проблема ABA. Есть ли такое в Go?
- [ ] ⭐ Copy-on-write конфиг: обновление без блокировок на чтении

🛠 [S · Кэш с TTL](sources/sobesrazborgoogle/README.md#кэш-с-ttl-in-memory) · [S · Pub/Sub](sources/sobesrazborgoogle/README.md#pubsub-брокер-в-памяти) · [S · Singleflight](sources/sobesrazborgoogle/README.md#singleflight--защита-от-эффекта-стада-cache-stampede) · ⭐[S · Шардированная map](sources/sobesrazborgoogle/README.md#шардированная-конкурентная-map-generics) · ⭐[S · Lock-free стек](sources/sobesrazborgoogle/README.md#lock-free-стек-трайбера-на-atomicpointer)

### 2.4 context
📖 [S · context.Context](sources/sobesrazborgoogle/README.md#contextcontext-в-go-отмена-таймауты-значения)

- [ ] Зачем нужен `context`? Какие методы у интерфейса?
- [ ] Чем отличаются все виды контекста: `Background`, `TODO`, `WithCancel`, `WithTimeout`, `WithDeadline`, `WithValue`, `WithCancelCause`, `WithoutCancel`, `AfterFunc`?
- [ ] Примеры применения каждого вида
- [ ] Почему обязательно вызывать `cancel()`?
- [ ] Правила использования (первый аргумент, не хранить в структуре, что можно класть в `Value`)
- [ ] Как работает `Value` и почему он медленный?
- [ ] Как отмена доходит до HTTP-клиента и БД?
- [ ] Как проверять отмену в горячем цикле?

🛠 ⭐[S · errgroup с лимитом](sources/sobesrazborgoogle/README.md#параллельные-запросы-с-лимитом-и-отменой-свой-errgroup) · P: ch-30

### 2.5 Память и GC
📖 [S · Runtime → «Стек и память», «Сборщик мусора»](sources/sobesrazborgoogle/README.md#runtime-go-планировщик-стек-escape-analysis-и-сборщик-мусора) · [GI · golang #17, #21](sources/go-interview/docs/golang/README.md) · 🌐 [A Guide to the Go GC](https://go.dev/doc/gc-guide)

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
📖 [S · Продвинутый Go](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior) · [S · Топ-10 Senior](sources/sobesrazborgoogle/README.md#топ-10-вопросов-senior-уровня)

- [ ] Инлайнинг: как работает, как контролировать?
- [ ] Bounds check elimination
- [ ] PGO (Profile-Guided Optimization)
- [ ] Какие директивы компилятора нужно знать?
- [ ] Как посмотреть, во что скомпилировался код?
- [ ] Правила `unsafe.Pointer`; `[]byte ↔ string` без копирования
- [ ] Насколько дорог reflect, когда оправдан? Как проверить тип переменной в runtime?
- [ ] Чем опасен cgo?
- [ ] Как писать код без лишних аллокаций в горячем пути?
- [ ] `runtime.ReadMemStats` vs `runtime/metrics`
- [ ] Монотонное время в `time.Time`

---

## Этап 3. Инструменты, прод, ОС

### 3.1 Модули и сборка
📖 [S · Основы #20](sources/sobesrazborgoogle/README.md#основы-go-вопросы-на-собеседовании-с-ответами) · [S · Продвинутый #25–27](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior)

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
📖 [S · Тестирование, бенчмарки и профилирование](sources/sobesrazborgoogle/README.md#тестирование-бенчмарки-и-профилирование-go)

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
- [ ] Бенчмарки
- [ ] Фаззинг
- [ ] `testing/synctest` (Go 1.25)
- [ ] Покрытие тестами
- [ ] TDD: почему тесты пишутся до кода? Как тесты влияют на организацию кода?

🛠 P: ch-16

### 3.3 Observability и troubleshooting
📖 [S · Тестирование… #8–10](sources/sobesrazborgoogle/README.md#тестирование-бенчмарки-и-профилирование-go) · [S · Архитектура #6](sources/sobesrazborgoogle/README.md#архитектура-go-сервисов-и-паттерны-проектирования) · [S · Продвинутый #21, #28](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior) · [GI · podolsky #15, #21–24](sources/go-interview/docs/podolsky/README.md) · 🌐 [Go Diagnostics](https://go.dev/doc/diagnostics) · 🌐 [OpenTelemetry Concepts](https://opentelemetry.io/docs/concepts/) · 🌐 [Prometheus metric types](https://prometheus.io/docs/concepts/metric_types/) · 🌐 SRE book: [SLO](https://sre.google/sre-book/service-level-objectives/), [Monitoring](https://sre.google/sre-book/monitoring-distributed-systems/)

- [ ] Что такое мониторинг и зачем он нужен?
- [ ] Логи, метрики, трейсинг, профилирование — что это и чем отличаются?
- [ ] Инструменты мониторинга (назови минимум 3)
- [ ] Уровни логов: когда какой использовать? Структурированное логирование (`log/slog`). Главный недостаток стандартного логгера?
- [ ] Типы метрик Prometheus (counter, gauge, histogram, summary). Стандартный набор метрик в Go-программе
- [ ] ⭐ Histogram vs summary: как считаются перцентили, почему нельзя усреднять p99?
- [ ] Что можно увидеть с помощью трейсинга? Distributed tracing, OpenTelemetry, context propagation
- [ ] Что такое APM (application performance management)?
- [ ] Методики RED / USE; four golden signals
- [ ] Алертинг: на что ставить алерты (симптомы vs причины)?
- [ ] pprof: какие профили бывают, как встроить в приложение, пример использования, overhead
- [ ] `go tool trace`, Flight Recorder
- [ ] Что такое debugging, breakpoint? Delve
- [ ] Что такое stdin, stdout, stderr?
- [ ] Как искать проблемы производительности на проде?
- [ ] Сервис ест много памяти или течёт — как расследовать по шагам?
- [ ] ⭐ p99 латентности растёт, а CPU-профиль «нормальный» — что делать?
- [ ] ⭐ Как отлаживать упавший или зависший процесс в проде?

🛠 [ТЗ Wolves](sources/Wolves/9.%20Troubleshooting%20%282%29.md): Go-приложение со всеми типами метрик Prometheus + стандартные метрики (CPU, heap, memory) → графики в Grafana, всё в docker-compose

### 3.4 🌐 Операционные системы и Linux
📖 🌐 [OSTEP](https://pages.cs.wisc.edu/~remzi/OSTEP/) (главы про процессы, виртуальную память, конкурентность, персистентность) · 🌐 [Brendan Gregg: Linux Performance](https://www.brendangregg.com/linuxperf.html) · 🌐 [The USE Method](https://www.brendangregg.com/usemethod.html)

- [ ] Процесс vs поток: что у них общее, что своё? Адресное пространство процесса (text, data, heap, stack)
- [ ] Виртуальная память: страницы, page fault, TLB, swap. Почему RSS ≠ VSZ?
- [ ] User space vs kernel space; что происходит при системном вызове?
- [ ] Файловые дескрипторы; «всё есть файл»; лимит `ulimit -n` и ошибка «too many open files»
- [ ] Модели ввода-вывода: блокирующий, неблокирующий, мультиплексирование (`select` / `poll` / `epoll` / `kqueue`). Как на этом построен netpoller Go? ⭐ io_uring
- [ ] Сигналы: SIGTERM vs SIGKILL vs SIGINT vs SIGHUP; обработка в Go (`os/signal`, `signal.NotifyContext`)
- [ ] Page cache и `fsync`: почему «записанные» данные могут потеряться при падении?
- [ ] Кэши CPU, cache line, локальность данных
- [ ] Zombie и orphan процессы; ⭐ PID 1 в контейнере
- [ ] cgroups и namespaces — на чём построены контейнеры
- [ ] OOM killer: когда приходит, как понять, что процесс убит им?
- [ ] Linux-инструменты: `top`/`htop`, `ps`, `lsof`, `ss`/`netstat`, `strace`, `tcpdump`, `df`/`du`, `free`, `vmstat`, `iostat`, `dmesg`, `journalctl`, `dig`, `curl`
- [ ] Как найти процесс, который занял порт? Что делать, если кончилось место на диске / дескрипторы / память?

### 3.5 Деплой, контейнеры, Kubernetes
📖 [GI · infrastructure_and_deploy](sources/go-interview/docs/infrastructure_and_deploy/README.md) · [S · System Design → «Концепции»](sources/sobesrazborgoogle/README.md#system-design-на-собеседовании-go-разработчика-middlesenior) · 🌐 [Docker overview](https://docs.docker.com/get-started/docker-overview/) · 🌐 [Multi-stage builds](https://docs.docker.com/build/building/multi-stage/) · 🌐 [Обзор Kubernetes (RU)](https://kubernetes.io/ru/docs/concepts/overview/)

- [ ] Blue-green deployment
- [ ] Canary-развёртывания
- [ ] Dark и A/B-развёртывания
- [ ] Rolling update; feature flags
- [ ] SLA, SLO, SLI, error budget
- [ ] Какие инструменты CI/CD знаешь?
- [ ] Как обеспечить непрерывность и стабильность деплоя?
- [ ] С какими проблемами при деплое сталкивался, как митигировал?
- [ ] 12-factor app
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

## Этап 4. Backend

### 4.1 Сети и протоколы
📖 [GI · common](sources/go-interview/docs/common/README.md) · [S · Backend → «HTTP», «gRPC»](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений) · 🌐 [High Performance Browser Networking](https://hpbn.co/) · 🌐 [what-happens-when](https://github.com/alex/what-happens-when)

- [ ] Уровни модели OSI (и TCP/IP)
- [ ] MAC-адрес vs IP-адрес; ⭐ подсети и CIDR
- [ ] TCP vs UDP; когда UDP предпочтительнее?
- [ ] 🌐 TCP: 3-way handshake, закрытие соединения, TIME_WAIT и CLOSE_WAIT (что значит много CLOSE_WAIT?)
- [ ] 🌐 Flow control vs congestion control
- [ ] Что такое сокет и порт? ⭐ `bind` / `listen` / `accept`
- [ ] Что такое NAT?
- [ ] Что такое DNS, как работает резолвинг? Что такое TTL записи?
- [ ] Что такое proxy? Forward vs reverse proxy
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
📖 [S · Backend → «HTTP»](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений)

- [ ] Как устроен сервер `net/http`?
- [ ] Что умеет `ServeMux` с Go 1.22?
- [ ] Middleware: как написать?
- [ ] Таймауты сервера и клиента
- [ ] Graceful shutdown
- [ ] Логирование запросов
- [ ] JSON: `encoding/json`, `encoding/json/v2`
- [ ] Фреймворки (gin, echo, fiber) — нужны ли?

🛠 [S · Graceful shutdown](sources/sobesrazborgoogle/README.md#graceful-shutdown-http-сервера) · P: ch-5, ch-9, ch-14 · `go-interview-practice/packages/` (gin, echo, fiber)

### 4.3 🌐 Проектирование API
📖 🌐 [Google API design guide](https://docs.cloud.google.com/apis/design) · 🌐 [AIP-158: Pagination](https://google.aip.dev/158) · 🌐 [Slack: Evolving API Pagination](https://slack.engineering/evolving-api-pagination-at-slack/) · 🌐 [Stripe: Idempotent requests](https://docs.stripe.com/api/idempotent_requests)

- [ ] REST vs gRPC vs GraphQL — когда что?
- [ ] Ресурсная модель: именование эндпоинтов, методы, коды ответов
- [ ] Версионирование API
- [ ] Пагинация: offset vs cursor/keyset — плюсы и минусы
- [ ] Идемпотентность: как реализовать idempotency key на сервере?
- [ ] Формат ошибок; какие коды возвращать
- [ ] Обратная совместимость: что можно и нельзя менять (в т.ч. номера полей в protobuf)
- [ ] Лимиты и квоты: `429`, `Retry-After`

### 4.4 🌐 Безопасность и аутентификация
📖 [S · Продвинутый #27](sources/sobesrazborgoogle/README.md#продвинутый-go-внутренности-рантайма-компилятор-unsafe-и-производительность-senior) · 🌐 [OWASP Top 10:2025](https://top10.owasp.org/2025/) · 🌐 [OWASP Password Storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html) · 🌐 [JWT Introduction](https://www.jwt.io/introduction) · 🌐 [OAuth 2.0](https://oauth.net/2/) · 🌐 [How OpenID Connect Works](https://openid.net/developers/how-connect-works/)

- [ ] Аутентификация vs авторизация
- [ ] Сессии и cookies vs токены
- [ ] JWT: структура, подпись (HS256 vs RS256), проблемы (отзыв, хранение); access + refresh токены
- [ ] OAuth 2.0: роли и flows (authorization code + PKCE, client credentials). Чем OIDC отличается от OAuth 2.0?
- [ ] Хранение паролей: соль, bcrypt / argon2id; почему не MD5 / SHA-256?
- [ ] OWASP Top 10: SQL injection, XSS, CSRF, SSRF, broken access control
- [ ] mTLS между сервисами
- [ ] Где хранить секреты (Vault, K8s Secrets); почему не в git?
- [ ] RBAC vs ABAC
- [ ] Go: `crypto/rand` vs `math/rand`, `html/template` и экранирование, `govulncheck`

🛠 P: ch-15

### 4.5 SQL и реляционные БД
📖 [GI · cache_and_db](sources/go-interview/docs/cache_and_db/README.md) · [S · Backend → «Базы данных»](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений)

- [ ] Что означает SQL? Какая БД является реляционной?
- [ ] Базовые команды SQL (DDL, DML)
- [ ] Что такое схема в БД?
- [ ] `ORDER BY`, `LIMIT X OFFSET Y` (и почему OFFSET плох на больших таблицах), `DISTINCT`
- [ ] `GROUP BY`, `HAVING`; WHERE vs HAVING; можно ли HAVING без группировки?
- [ ] Виды JOIN; JOIN с подзапросами; коррелированный подзапрос; `EXISTS` vs `IN`
- [ ] `UNION` vs `UNION ALL`
- [ ] `INSERT ... ON CONFLICT` (upsert), `RETURNING`
- [ ] Виды связей между таблицами; как реализовать many-to-many?
- [ ] Нормализация, первые 3 НФ. Когда нужна денормализация?
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
📖 [GI · cache_and_db](sources/go-interview/docs/cache_and_db/README.md) · [S · Backend #13](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений) · 🌐 [PG: Index Types](https://www.postgresql.org/docs/current/indexes-types.html) · 🌐 [PG: Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html) ([RU](https://postgrespro.ru/docs/postgresql/current/using-explain))

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
- [ ] `EXPLAIN` vs `EXPLAIN ANALYZE`
- [ ] 🌐 `CREATE INDEX CONCURRENTLY` → [PG docs](https://www.postgresql.org/docs/current/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY) ([RU](https://postgrespro.ru/docs/postgresql/current/sql-createindex#SQL-CREATEINDEX-CONCURRENTLY))
- [ ] 🌐 GIN, GiST, BRIN индексы → [PG: Index Types](https://www.postgresql.org/docs/current/indexes-types.html); RUM → [postgrespro/rum](https://github.com/postgrespro/rum)
- [ ] Есть ли индексы только в реляционных БД?

### 4.7 Транзакции и блокировки
📖 [S · Backend #12](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений) · [GI · cache_and_db → «дедлоки»](sources/go-interview/docs/cache_and_db/README.md) · 🌐 [PG: Concurrency Control](https://www.postgresql.org/docs/current/mvcc.html) · 🌐 [Изоляция транзакций (RU)](https://postgrespro.ru/docs/postgresql/current/transaction-iso) · 🌐 [PG: Explicit Locking](https://www.postgresql.org/docs/current/explicit-locking.html)

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
📖 [GI · cache_and_db](sources/go-interview/docs/cache_and_db/README.md) · [S · System Design → «Концепции»](sources/sobesrazborgoogle/README.md#system-design-на-собеседовании-go-разработчика-middlesenior) · 🌐 PG: [Streaming Replication](https://www.postgresql.org/docs/current/warm-standby.html#STREAMING-REPLICATION), [Logical Replication](https://www.postgresql.org/docs/current/logical-replication.html), [Partitioning](https://www.postgresql.org/docs/current/ddl-partitioning.html)

- [ ] Horizontal vs vertical scaling
- [ ] Что такое репликация? Sync vs async; master-slave, multi-leader, leaderless (кворумы `R + W > N`)
- [ ] Логическая vs физическая репликация
- [ ] Лаг репликации: как обеспечить read-your-writes при чтении с реплик?
- [ ] ⭐ Failover: как происходит переключение на реплику?
- [ ] Что такое partitioning? Требования к ключу партиционирования
- [ ] Что такое sharding? Подходы: range, hash, consistent hashing; решардинг
- [ ] CAP / PACELC

### 4.10 Go и БД
📖 [S · Backend #10–15](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений) · [GI · podolsky #16](sources/go-interview/docs/podolsky/README.md)

- [ ] `database/sql`: пул соединений и его настройки
- [ ] Типичные утечки (незакрытые `rows` и т.п.)
- [ ] N+1, SQL-инъекции, prepared statements
- [ ] Есть ли в Go хороший ORM? sqlx, pgx, gorm, sqlc — плюсы и минусы
- [ ] Транзакции в Go: `defer tx.Rollback()`, как прокинуть транзакцию через слои
- [ ] Миграции; миграции без даунтайма (expand / contract, новая колонка `NOT NULL`, индекс на живой таблице)

🛠 P: ch-13 · `go-interview-practice/packages/` (gorm, mongodb)

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
📖 [S · Backend #18](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений) · [S · System Design](sources/sobesrazborgoogle/README.md#system-design-на-собеседовании-go-разработчика-middlesenior) · 🌐 Redis: [data types](https://redis.io/docs/latest/develop/data-types/), [persistence](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/), [eviction](https://redis.io/docs/latest/develop/reference/eviction/)

- [ ] Стратегии кэширования: cache-aside, write-through, write-back; инвалидация; TTL с jitter
- [ ] Консистентность кэша и БД: в каком порядке обновлять и инвалидировать?
- [ ] Cache stampede: что это и как защититься?
- [ ] Redis: структуры данных, persistence (RDB / AOF), eviction-политики, почему однопоточный Redis быстрый?
- [ ] Горячие ключи и большие ключи — чем опасны?
- [ ] ⭐ Redis Sentinel vs Redis Cluster
- [ ] ⭐ Pub/Sub и Streams в Redis
- [ ] ⭐ 🌐 Распределённая блокировка на Redis — что может пойти не так? → [Redis: Distributed Locks](https://redis.io/docs/latest/develop/clients/patterns/distributed-locks/), [Kleppmann: How to do distributed locking](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html)

🛠 [S · Кэш с TTL](sources/sobesrazborgoogle/README.md#кэш-с-ttl-in-memory) · [S · Singleflight](sources/sobesrazborgoogle/README.md#singleflight--защита-от-эффекта-стада-cache-stampede) · P: ch-28

### 4.13 Брокеры сообщений
📖 [S · Backend #16–17](sources/sobesrazborgoogle/README.md#go-backend-на-собеседовании-http-grpc-базы-данных-брокеры-сообщений) · 🌐 [Kafka Docs: Design](https://kafka.apache.org/43/design/design/) · 🌐 [Kafka: The Definitive Guide](https://www.confluent.io/resources/ebook/kafka-the-definitive-guide/) (бесплатно после регистрации) · 🌐 [RabbitMQ: AMQP 0-9-1 Model](https://www.rabbitmq.com/tutorials/amqp-concepts)

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
- [ ] Outbox pattern
- [ ] Ретраи, dead letter queue, «ядовитые» сообщения

🛠 [S · Батчер](sources/sobesrazborgoogle/README.md#батчер-пачка-по-размеру-или-по-времени) · [S · Pub/Sub](sources/sobesrazborgoogle/README.md#pubsub-брокер-в-памяти)

---

## Этап 5. Архитектура и системы

### 5.1 ООП и принципы проектирования
📖 [S · Архитектура #2, #4](sources/sobesrazborgoogle/README.md#архитектура-go-сервисов-и-паттерны-проектирования) · [GI · README → «шаблоны проектирования», «организация кода»](sources/go-interview/README.md)

- [ ] Что такое ООП? Принципы: инкапсуляция, наследование, полиморфизм (+ абстракция)
- [ ] Как принципы ООП реализуются в Go без классов и наследования?
- [ ] SOLID: общее определение и каждый принцип с примером на Go
- [ ] DRY, WET, KISS, YAGNI
- [ ] ООП vs функциональное программирование
- [ ] 🌐 Компонентно-ориентированное программирование → [Википедия](https://ru.wikipedia.org/wiki/%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)
- [ ] Сцепление (coupling) vs связность (cohesion)
- [ ] Какие паттерны знаешь? Builder, Factory, Singleton, Adapter, Decorator, Strategy, Observer. Какие применял?

### 5.2 Архитектура сервиса
📖 [S · Архитектура](sources/sobesrazborgoogle/README.md#архитектура-go-сервисов-и-паттерны-проектирования)

- [ ] Структура Go-проекта
- [ ] Что такое чистая архитектура? Какие в ней слои?
- [ ] Как применить инверсию зависимостей в чистой архитектуре?
- [ ] Гексагональная архитектура (ports & adapters)
- [ ] Dependency Injection в Go
- [ ] DDD: bounded context, агрегаты, entity vs value object
- [ ] DDD, BDD, TDD — в чём разница?
- [ ] CQRS; Event Sourcing — когда оправданы?
- [ ] Модульный монолит

### 5.3 Микросервисы
📖 [GI · microservices](sources/go-interview/docs/microservices/README.md) · [S · Архитектура #5](sources/sobesrazborgoogle/README.md#архитектура-go-сервисов-и-паттерны-проектирования)

- [ ] Что такое микросервисная архитектура?
- [ ] Монолит vs микросервисы: плюсы и минусы
- [ ] Как делить систему на сервисы? Признаки неудачного деления (distributed monolith)
- [ ] Способы общения сервисов: синхронные (REST, gRPC) и асинхронные (брокеры)
- [ ] Паттерн Saga: хореография vs оркестрация
- [ ] API Gateway, service discovery; ⭐ service mesh
- [ ] Как тестировать распределённую систему?

### 5.4 Надёжность и распределённые системы
📖 [S · Распределённые системы](sources/sobesrazborgoogle/README.md#распределённые-системы-и-надёжность-вопросы-senior-go-разработчику) · 🌐 [Kleppmann: Distributed Systems (лекции, PDF)](https://www.cl.cam.ac.uk/teaching/2122/ConcDisSys/dist-sys-notes.pdf) · 🌐 [Raft](https://raft.github.io/) · 🌐 [DDIA](https://dataintensive.net/)

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

🛠 [S · Circuit Breaker](sources/sobesrazborgoogle/README.md#circuit-breaker-на-go) · [S · Rate Limiter](sources/sobesrazborgoogle/README.md#rate-limiter-token-bucket) · [S · Retry](sources/sobesrazborgoogle/README.md#retry-с-экспоненциальной-задержкой-и-jitter) · [S · Consistent hashing](sources/sobesrazborgoogle/README.md#consistent-hashing-с-виртуальными-узлами) · P: ch-20, ch-29

### 5.5 System Design
📖 [S · System Design](sources/sobesrazborgoogle/README.md#system-design-на-собеседовании-go-разработчика-middlesenior) · 🌐 [system-design-primer](https://github.com/donnemartin/system-design-primer) · 🌐 [ByteByteGo system-design-101](https://github.com/ByteByteGoHq/system-design-101)

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
- [ ] Распределённый планировщик задач (cron)
- [ ] Система сбора метрик / логов
- [ ] Web crawler

---

## Этап 6. Практика

### 6.1 🌐 Алгоритмы и структуры данных
📖 🌐 [Яндекс Хендбук «Основы алгоритмов»](https://contest.yandex.ru/tracks/algorithms) · 🌐 [Яндекс «Тренировки по алгоритмам»](https://yandex.ru/yaintern/training/algorithm-training) · 🌐 [NeetCode Roadmap](https://neetcode.io/roadmap) / [NeetCode 150](https://neetcode.io/practice/practice/neetcode150) · 🌐 [LeetCode Top Interview 150](https://leetcode.com/studyplan/top-interview-150/) · [S · задачи](sources/sobesrazborgoogle/README.md#задачи-с-go-собеседований-решения-разборы-и-тесты)

Теория:
- [ ] Big-O по времени и памяти; амортизированная сложность (почему `append` — O(1) в среднем)
- [ ] Сортировки: quick, merge, heap, counting; стабильность; что использует `slices.Sort` (pdqsort)
- [ ] Структуры данных и сложность операций: массив, связный список, стек, очередь, дек, хеш-таблица, куча, дерево, граф, trie

Паттерны (на каждый решить 3–5 задач):
- [ ] Два указателя
- [ ] Скользящее окно · [S · Longest Substring](sources/sobesrazborgoogle/README.md#longest-substring-without-repeating-characters)
- [ ] Префиксные суммы
- [ ] Хеш-таблица: подсчёт, группировка · [S · Two Sum](sources/sobesrazborgoogle/README.md#two-sum--найти-два-числа-с-заданной-суммой), [S · Group Anagrams](sources/sobesrazborgoogle/README.md#group-anagrams--группировка-анаграмм)
- [ ] Стек; монотонный стек · [S · Скобочная последовательность](sources/sobesrazborgoogle/README.md#правильная-скобочная-последовательность)
- [ ] Бинарный поиск, в т.ч. по ответу · [S · Бинарный поиск](sources/sobesrazborgoogle/README.md#бинарный-поиск-lower-bound-и-сдвинутый-массив) · P: ch-21
- [ ] Связные списки (fast / slow указатели) · [S · Связный список](sources/sobesrazborgoogle/README.md#связный-список-разворот-цикл-середина-слияние)
- [ ] Деревья: обходы DFS / BFS, BST, высота, LCA
- [ ] Куча, top-K (`container/heap`) · [S · Top K](sources/sobesrazborgoogle/README.md#top-k-frequent--k-самых-частых-элементов)
- [ ] Интервалы, sweep line · [S · Merge Intervals](sources/sobesrazborgoogle/README.md#merge-intervals--слияние-отрезков)
- [ ] Графы: BFS / DFS, топологическая сортировка, компоненты связности, поиск цикла, Dijkstra · P: ch-25
- [ ] Backtracking: перестановки, подмножества, комбинации
- [ ] Динамическое программирование: 1D, 2D, рюкзак, LIS, LCS · P: ch-24
- [ ] Жадные алгоритмы · P: ch-22
- [ ] Битовые операции
- [ ] ⭐ Union-Find, Trie

Как решать на собесе:
- [ ] Уточнить условие и граничные случаи → озвучить идею и сложность → написать код → прогнать тесты руками
- [ ] Уметь писать без автодополнения и без запуска кода

### 6.2 Live coding на конкурентность
📖 [S · задачи → «Конкурентность»](sources/sobesrazborgoogle/README.md#задачи-с-go-собеседований-решения-разборы-и-тесты) · [GI · popular_tasks](sources/go-interview/docs/popular_tasks/README.md)

- [ ] [Worker pool](sources/sobesrazborgoogle/README.md#worker-pool-на-go)
- [ ] [Fan-in: слить N каналов](sources/sobesrazborgoogle/README.md#fan-in-слить-n-каналов-в-один)
- [ ] [Pipeline](sources/sobesrazborgoogle/README.md#pipeline-конвейер-на-каналах)
- [ ] [Первый успешный ответ из N реплик](sources/sobesrazborgoogle/README.md#первый-успешный-ответ-из-n-реплик-с-таймаутом)
- [ ] Параллельно обойти N URL с лимитом, таймаутом и отменой по первой ошибке · [S · свой errgroup](sources/sobesrazborgoogle/README.md#параллельные-запросы-с-лимитом-и-отменой-свой-errgroup)
- [ ] [Кэш с TTL](sources/sobesrazborgoogle/README.md#кэш-с-ttl-in-memory)
- [ ] [Rate limiter](sources/sobesrazborgoogle/README.md#rate-limiter-token-bucket)
- [ ] [Graceful shutdown](sources/sobesrazborgoogle/README.md#graceful-shutdown-http-сервера)
- [ ] [Батчер](sources/sobesrazborgoogle/README.md#батчер-пачка-по-размеру-или-по-времени)
- [ ] [Pub/Sub](sources/sobesrazborgoogle/README.md#pubsub-брокер-в-памяти)
- [ ] [Singleflight](sources/sobesrazborgoogle/README.md#singleflight--защита-от-эффекта-стада-cache-stampede)
- [ ] Кастомная WaitGroup на семафоре · [GI · popular_tasks #6](sources/go-interview/docs/popular_tasks/README.md)
- [ ] Параллельно читать из кэша и БД, вернуть первый успешный ответ (Ozon)
- [ ] Краулер: обойти сайт по sitemap через BFS, потом распараллелить с лимитом (Яндекс)
- [ ] In-memory «топ новостей» с конкурентным доступом (VK)
- [ ] Клиентский балансировщик с retry, health-check и circuit breaker (Яндекс)
- [ ] ⭐ [Circuit breaker](sources/sobesrazborgoogle/README.md#circuit-breaker-на-go), [Retry с jitter](sources/sobesrazborgoogle/README.md#retry-с-экспоненциальной-задержкой-и-jitter)

### 6.3 Code review секция
📖 [S · Как проходит собеседование → «Code review»](sources/sobesrazborgoogle/README.md#как-проходит-собеседование-go-разработчика-в-2026-году) · 🌐 [100 Go Mistakes](https://100go.co/)

Уметь найти в чужом коде:
- [ ] Гонку при записи в map / `append` / общую переменную из горутин
- [ ] Утечку горутин (нет выхода, блокировка на канале без читателя)
- [ ] Незакрытые `resp.Body`, `rows`, файлы
- [ ] Проигнорированные ошибки; ошибки без контекста
- [ ] `defer` в цикле
- [ ] Захват переменной цикла (если в `go.mod` версия < 1.22)
- [ ] Типизированный nil в интерфейсе ошибки
- [ ] Копирование структуры с `sync.Mutex` (value receiver)
- [ ] `http.Client` без таймаута; `context.Background()` вместо входящего ctx
- [ ] SQL через `fmt.Sprintf` (инъекция)
- [ ] `wg.Add` внутри горутины; канал закрывает не владелец или несколько писателей
- [ ] Паника в горутине без `recover` роняет весь процесс
- [ ] Запись в nil-map
- [ ] Неограниченное число горутин
- [ ] Лишние аллокации: конкатенация в цикле, слайс без предвыделения
- [ ] Читаемость: именование, магические числа, огромные функции, нет тестов
- [ ] Порядок ответа: корректность → конкурентность → ресурсы → ошибки → производительность → читаемость

### 6.4 «Что выведет код»
- [ ] [S · 25 задач](sources/sobesrazborgoogle/README.md#что-выведет-этот-код--25-каверзных-задач-по-go-с-собеседований)
- [ ] ⭐ [S · Senior: ещё 15](sources/sobesrazborgoogle/README.md#что-выведет-этот-код--senior-уровень-ещё-15-задач)
- [ ] [GI · popular_tasks #7–10](sources/go-interview/docs/popular_tasks/README.md)

---

## Этап 7. Перед собеседованием

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

**Что общее почти у всех:**
- [ ] Писать код без IDE, без запуска и без ИИ → тренируйся в простом редакторе (6.1, 6.2)
- [ ] Код-ревью Go-кода (6.3) и задачи на конкурентность (6.2)
- [ ] Troubleshooting: «куда уходит память», «почему тормозит» (3.3, 3.4)
- [ ] SQL вживую, иногда с запуском запросов (4.5)
- [ ] В system design считать нагрузку и мощности: RPS, объёмы, latency numbers (5.5)

### 7.2 Поведенческие вопросы и секция о проектах
📖 [S · Как проходит собеседование → «Поведенческие вопросы»](sources/sobesrazborgoogle/README.md#как-проходит-собеседование-go-разработчика-в-2026-году)

Подготовить истории по STAR (ситуация → задача → действия → результат):
- [ ] Расскажи о себе (2 минуты)
- [ ] Архитектура последнего проекта: нарисовать, объяснить решения, узкие места, что будет при нагрузке ×10
- [ ] Самый сложный баг или инцидент в проде: как нашёл, как починил, что изменили после
- [ ] Конфликт или несогласие с решением в команде
- [ ] Ошибка или провал и что вынес
- [ ] Инициатива: что улучшил сам, без запроса
- [ ] Трейд-офф: когда осознанно выбрал «хуже, но быстрее»
- [ ] Почему уходишь / почему к нам
- [ ] Свои вопросы к интервьюеру

### 7.3 Финальный прогон
- [ ] [S · Что нового в Go 1.22–1.27](sources/sobesrazborgoogle/README.md#что-нового-в-go-122127-шпаргалка-к-собеседованию-2026)
- [ ] [S · Как проходит собеседование](sources/sobesrazborgoogle/README.md#как-проходит-собеседование-go-разработчика-в-2026-году): этапы, что оценивают на live coding
- [ ] [S · Чек-лист подготовки](sources/sobesrazborgoogle/README.md#чек-лист-подготовки-к-собеседованию-go-разработчика)
- [ ] Mock-интервью: минимум одно по алгоритмам, одно по Go и одно по system design

---

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

**Прочее**
- [Pro Git (RU)](https://git-scm.com/book/ru/v2) · [OWASP Top 10](https://top10.owasp.org/2025/) · [Google API design guide](https://docs.cloud.google.com/apis/design) · [Kubernetes docs](https://kubernetes.io/ru/docs/concepts/overview/) · [Docker docs](https://docs.docker.com/get-started/docker-overview/)
