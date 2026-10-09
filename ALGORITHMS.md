# 🧩 Алгоритмы на Go: 100 задач и шаблоны

[← к роадмапу](ROADMAP.md#s6-1) · [README](README.md)

100 задач с LeetCode по 17 паттернам, план на 8 недель и шаблоны решений на Go. Основа — NeetCode 150 плюс задачи, которые часто дают на русскоязычных собесах. Все задачи бесплатные, без Premium. Код шаблонов проверен тестами на Go 1.26.

**Обозначения**
- ★ — база: 55 задач, минимум перед собесом
- 🟢 Easy · 🟡 Medium · 🔴 Hard — по оценке LeetCode. Всего: 🟢 23 · 🟡 68 · 🔴 9
- 🔥 — эта задача или её вариант часто встречается на русскоязычных собесах
- 💡 Подсказки под каждым разделом свёрнуты: сначала реши сам

**Содержание:** [Как заниматься](#how) · [План на 8 недель](#plan) · [Go для алгоритмов](#go) · [Шаблоны](#templates) · [Задачи по паттернам](#tasks)

---

<a id="how"></a>
## 🧭 Как заниматься

- **Время.** На Medium — 30–40 минут. Не получается — открой разбор (Editorial на LeetCode или видео NeetCode), разберись и через 2–3 дня реши задачу заново без подсказок.
- **Как на собесе.** Пиши в простом редакторе без автодополнения и не запускай код, пока не прогонишь пример руками. Так проходят секции в Яндексе и многих других компаниях ([форматы собесов](ROADMAP.md#s7-1)).
- **Вслух.** Условие и граничные случаи → идея → сложность → код → прогон на примере. Подробнее — в [6.1](ROADMAP.md#s6-1).
- **Сложность.** После каждого решения называй сложность по времени и памяти.
- **Отметки.** `[x]` — только если решил без подсказки. Решённую с подсказкой задачу верни в повтор.
- Задачи на конкурентность в Go — отдельно, в [6.2](ROADMAP.md#s6-2).

---

<a id="plan"></a>
## 📅 План на 8 недель

По 2 задачи в день, параллельно с теорией. Первые 4 недели — только база ★ по всем паттернам, следующие 4 — остальные задачи и повтор.

| Неделя | Что | Темы | Задач |
|:---:|---|---|:---:|
| 1 | ★ база | [Массивы и хеширование](#t-arrays), [Два указателя](#t-two-pointers), [Скользящее окно](#t-window), [Префиксные суммы](#t-prefix) | 15 |
| 2 | ★ база | [Строки](#t-strings), [Стек и монотонный стек](#t-stack), [Бинарный поиск](#t-binary-search), [Связные списки](#t-linked-list) | 13 |
| 3 | ★ база | [Деревья](#t-trees), [Куча, top-K](#t-heap), [Рекурсия и backtracking](#t-backtracking), [Жадные алгоритмы](#t-greedy) | 13 |
| 4 | ★ база | [Графы](#t-graphs), [Интервалы](#t-intervals), [Динамическое программирование](#t-dp), [Биты, математика, матрицы](#t-bits-math) | 14 |
| 5 | остальные | [Массивы и хеширование](#t-arrays), [Два указателя](#t-two-pointers), [Скользящее окно](#t-window), [Префиксные суммы](#t-prefix), [Строки](#t-strings), [Стек и монотонный стек](#t-stack), [Бинарный поиск](#t-binary-search) | 12 |
| 6 | остальные | [Связные списки](#t-linked-list), [Деревья](#t-trees), [Куча, top-K](#t-heap), [Рекурсия и backtracking](#t-backtracking) | 12 |
| 7 | остальные | [Графы](#t-graphs), [Интервалы](#t-intervals), [Жадные алгоритмы](#t-greedy), [Trie ⭐](#t-trie) | 13 |
| 8 | остальные + повтор | [Динамическое программирование](#t-dp), [Биты, математика, матрицы](#t-bits-math) | 8 |

Дальше — смешанные задачи без подсказки о паттерне: [NeetCode 150](https://neetcode.io/practice) целиком, [Яндекс «Тренировки по алгоритмам»](https://yandex.ru/yaintern/training/algorithm-training), и минимум одно mock-интервью по алгоритмам ([7.3](ROADMAP.md#stage-7)).

---

<a id="go"></a>
## 🐹 Go для алгоритмов

| Нужно | В Go |
|---|---|
| Сортировка | `slices.Sort(a)`; по полю — `slices.SortFunc(a, func(x, y T) int { return cmp.Compare(x.F, y.F) })`; стабильная — `slices.SortStableFunc` |
| Бинарный поиск | `slices.BinarySearch(a, x)` → индекс и «найден ли»; `sort.Search(n, f)` — первый `i`, где `f(i)` истинно |
| Минимум, максимум | встроенные `min` и `max` (Go 1.21), `math.MaxInt`, `math.MinInt`; модуль для `int` — своя функция |
| Множество | `map[T]struct{}`; для букв — `[26]bool` |
| Счётчик | `[26]int` для букв (быстрее map), иначе `map[T]int` |
| Составной ключ | массив или структура: `map[[2]int]bool` |
| Стек | слайс: `append`, снять — `s = s[:len(s)-1]` |
| Очередь | слайс: `append`, снять — `q = q[1:]` |
| Дек | `container/list` или кольцевой буфер на слайсе |
| Куча | `container/heap`: тип с пятью методами ([шаблон 9](#tpl-9)) |
| Строки | `s[i]` — байт; `[]byte(s)` — чтобы менять; `[]rune(s)` — для Unicode; сборка — `strings.Builder` |
| Числа ↔ строки | `strconv.Itoa`, `strconv.Atoi` |
| Биты | `bits.OnesCount`, `bits.Len`, `bits.TrailingZeros` из `math/bits` |
| Двумерный слайс | `make([][]int, n)`, затем каждая строка — `make([]int, m)` |

**⚠️ Подвохи Go**
- **Backtracking и `append`.** Сохраняй копию: `res = append(res, slices.Clone(path))`. Без копии все ответы делят один массив: `subsets([1 2 3])` вернёт `[[] [2] [2] [1 2] [1] [1 2] [1 2] [1 2 3]]` вместо `[[] [3] [2] [2 3] [1] [1 3] [1 2] [1 2 3]]`.
- **Рекурсивное замыкание.** Сначала `var dfs func(int)`, потом `dfs = func(i int) { … dfs(i + 1) … }`.
- **Порядок `range` по map случайный.** Если ответ зависит от порядка — сортируй.
- **Переполнение.** `int` 64-битный; середину считай как `lo + (hi-lo)/2`; в задачах «по модулю 10⁹+7» бери модуль на каждом шаге.
- **Строки.** `s += x` в цикле — O(n²), собирай через `strings.Builder` или `[]byte`.
- **Очередь на слайсе.** `q = q[1:]` не освобождает память в начале массива — для задачи это нормально.
- **Глубокая рекурсия.** Стек горутины растёт сам до лимита 1 ГБ на 64-битных системах. Глубина 10⁵ — нормально, для 10⁶ и больше лучше итеративно.
- **Ввод в контестах** (Яндекс Контест и подобные): `fmt.Scan` без буфера медленный, используй `bufio` ([шаблон 1](#tpl-1)).

---

<a id="templates"></a>
## 🧱 Шаблоны

Импорты опущены. Все шаблоны покрыты тестами.

<a id="tpl-1"></a>
<details>
<summary><b>1. Ввод-вывод для контеста</b> — <code>bufio</code> вместо <code>fmt.Scan</code></summary>

```go
func main() {
	in := bufio.NewReader(os.Stdin)
	out := bufio.NewWriter(os.Stdout)
	defer out.Flush() // без Flush вывод потеряется

	var n int
	fmt.Fscan(in, &n)
	a := make([]int, n)
	for i := range a {
		fmt.Fscan(in, &a[i])
	}
	sum := 0
	for _, x := range a {
		sum += x
	}
	fmt.Fprintln(out, sum)
}
```

Ввод из 200 000 чисел читается меньше чем за секунду вместе с запуском.

</details>

<a id="tpl-2"></a>
<details>
<summary><b>2. Бинарный поиск</b> — lower bound и поиск по ответу</summary>

```go
// lowerBound — первый индекс i, где a[i] >= x (или len(a), если таких нет).
func lowerBound(a []int, x int) int {
	lo, hi := 0, len(a)
	for lo < hi {
		mid := lo + (hi-lo)/2
		if a[mid] < x {
			lo = mid + 1
		} else {
			hi = mid
		}
	}
	return lo
}

// searchAnswer — минимальное v в [lo, hi], для которого ok(v) == true.
// ok должна быть монотонной: false, false, …, true, true.
func searchAnswer(lo, hi int, ok func(int) bool) int {
	for lo < hi {
		mid := lo + (hi-lo)/2
		if ok(mid) {
			hi = mid
		} else {
			lo = mid + 1
		}
	}
	return lo
}
```

Поиск по ответу, пример — Koko Eating Bananas: `ok(v)` считает, сколько часов уйдёт при скорости `v`, и сравнивает с `h`. Ответ — `searchAnswer(1, slices.Max(piles), ok)`.

</details>

<a id="tpl-3"></a>
<details>
<summary><b>3. Два указателя</b> — с двух концов отсортированного массива</summary>

```go
// twoSumSorted — индексы пары с суммой target в отсортированном слайсе.
func twoSumSorted(a []int, target int) (int, int) {
	l, r := 0, len(a)-1
	for l < r {
		switch s := a[l] + a[r]; {
		case s == target:
			return l, r
		case s < target:
			l++
		default:
			r--
		}
	}
	return -1, -1
}
```

</details>

<a id="tpl-4"></a>
<details>
<summary><b>4. Скользящее окно</b> — окно переменной длины</summary>

```go
// lengthOfLongestSubstring — самая длинная подстрока без повторов.
func lengthOfLongestSubstring(s string) int {
	last := map[byte]int{} // символ → последняя позиция
	best, left := 0, 0
	for right := 0; right < len(s); right++ {
		if i, ok := last[s[right]]; ok && i >= left {
			left = i + 1 // сдвигаем левую границу за повтор
		}
		last[s[right]] = right
		best = max(best, right-left+1)
	}
	return best
}
```

Схема: двигаем правую границу; окно стало невалидным — подтягиваем левую; обновляем ответ.

</details>

<a id="tpl-5"></a>
<details>
<summary><b>5. Префиксные суммы + map</b> — подмассивы с заданной суммой</summary>

```go
// subarraySum — число подмассивов с суммой k.
func subarraySum(a []int, k int) int {
	cnt := map[int]int{0: 1} // префиксная сумма → сколько раз встречалась
	sum, res := 0, 0
	for _, x := range a {
		sum += x
		res += cnt[sum-k]
		cnt[sum]++
	}
	return res
}
```

</details>

<a id="tpl-6"></a>
<details>
<summary><b>6. Монотонный стек</b> — ближайший больший или меньший элемент</summary>

```go
// dailyTemperatures — через сколько дней станет теплее.
func dailyTemperatures(t []int) []int {
	res := make([]int, len(t))
	var st []int // индексы; температуры в стеке убывают
	for i, x := range t {
		for len(st) > 0 && t[st[len(st)-1]] < x {
			j := st[len(st)-1]
			st = st[:len(st)-1]
			res[j] = i - j
		}
		st = append(st, i)
	}
	return res
}
```

</details>

<a id="tpl-7"></a>
<details>
<summary><b>7. BFS по сетке</b> — кратчайший путь в невзвешенном графе</summary>

```go
var dirs = [4][2]int{{1, 0}, {-1, 0}, {0, 1}, {0, -1}}

// bfs — расстояния от (sr, sc) до всех клеток; '#' — стена, -1 — недостижимо.
func bfs(grid []string, sr, sc int) [][]int {
	n, m := len(grid), len(grid[0])
	dist := make([][]int, n)
	for i := range dist {
		dist[i] = make([]int, m)
		for j := range dist[i] {
			dist[i][j] = -1
		}
	}
	dist[sr][sc] = 0
	q := [][2]int{{sr, sc}}
	for len(q) > 0 {
		cur := q[0]
		q = q[1:]
		for _, d := range dirs {
			r, c := cur[0]+d[0], cur[1]+d[1]
			if r < 0 || r >= n || c < 0 || c >= m || grid[r][c] == '#' || dist[r][c] != -1 {
				continue
			}
			dist[r][c] = dist[cur[0]][cur[1]] + 1
			q = append(q, [2]int{r, c})
		}
	}
	return dist
}
```

</details>

<a id="tpl-8"></a>
<details>
<summary><b>8. Топологическая сортировка</b> — алгоритм Кана и поиск цикла</summary>

```go
// topoSort — порядок вершин 0..n-1 (алгоритм Кана) или nil, если есть цикл.
func topoSort(n int, edges [][2]int) []int {
	g := make([][]int, n)
	indeg := make([]int, n)
	for _, e := range edges {
		g[e[0]] = append(g[e[0]], e[1])
		indeg[e[1]]++
	}
	var q, order []int
	for v := range n {
		if indeg[v] == 0 {
			q = append(q, v)
		}
	}
	for len(q) > 0 {
		v := q[0]
		q = q[1:]
		order = append(order, v)
		for _, u := range g[v] {
			indeg[u]--
			if indeg[u] == 0 {
				q = append(q, u)
			}
		}
	}
	if len(order) < n {
		return nil
	}
	return order
}
```

</details>

<a id="tpl-9"></a>
<details>
<summary><b>9. Куча: top-K</b> — <code>container/heap</code></summary>

```go
// IntHeap — min-куча для container/heap.
type IntHeap []int

func (h IntHeap) Len() int           { return len(h) }
func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] } // > — max-куча
func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }
func (h *IntHeap) Push(x any)        { *h = append(*h, x.(int)) }
func (h *IntHeap) Pop() any {
	old := *h
	x := old[len(old)-1]
	*h = old[:len(old)-1]
	return x
}

// kthLargest — k-й по величине: держим min-кучу из k самых больших.
func kthLargest(a []int, k int) int {
	h := &IntHeap{}
	for _, x := range a {
		heap.Push(h, x)
		if h.Len() > k {
			heap.Pop(h)
		}
	}
	return (*h)[0]
}
```

</details>

<a id="tpl-10"></a>
<details>
<summary><b>10. Dijkstra</b> — кратчайшие пути с неотрицательными весами</summary>

```go
type Edge struct{ to, w int }
type Item struct{ v, d int }
type PQ []Item

func (h PQ) Len() int           { return len(h) }
func (h PQ) Less(i, j int) bool { return h[i].d < h[j].d }
func (h PQ) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }
func (h *PQ) Push(x any)        { *h = append(*h, x.(Item)) }
func (h *PQ) Pop() any {
	old := *h
	x := old[len(old)-1]
	*h = old[:len(old)-1]
	return x
}

// dijkstra — кратчайшие расстояния от src; веса неотрицательные.
func dijkstra(g [][]Edge, src int) []int {
	dist := make([]int, len(g))
	for i := range dist {
		dist[i] = math.MaxInt
	}
	dist[src] = 0
	h := &PQ{{src, 0}}
	for h.Len() > 0 {
		cur := heap.Pop(h).(Item)
		if cur.d > dist[cur.v] {
			continue // устаревшая запись
		}
		for _, e := range g[cur.v] {
			if nd := cur.d + e.w; nd < dist[e.to] {
				dist[e.to] = nd
				heap.Push(h, Item{e.to, nd})
			}
		}
	}
	return dist
}
```

</details>

<a id="tpl-11"></a>
<details>
<summary><b>11. Union-Find</b> — компоненты связности, лишние рёбра</summary>

```go
// DSU — система непересекающихся множеств (Union-Find).
type DSU struct{ parent, size []int }

func NewDSU(n int) *DSU {
	d := &DSU{make([]int, n), make([]int, n)}
	for i := range n {
		d.parent[i], d.size[i] = i, 1
	}
	return d
}

func (d *DSU) Find(x int) int {
	for d.parent[x] != x {
		d.parent[x] = d.parent[d.parent[x]] // сжатие пути
		x = d.parent[x]
	}
	return x
}

// Union объединяет множества; false — если a и b уже в одном.
func (d *DSU) Union(a, b int) bool {
	a, b = d.Find(a), d.Find(b)
	if a == b {
		return false
	}
	if d.size[a] < d.size[b] {
		a, b = b, a
	}
	d.parent[b] = a
	d.size[a] += d.size[b]
	return true
}
```

</details>

<a id="tpl-12"></a>
<details>
<summary><b>12. Trie</b> — префиксное дерево</summary>

```go
// Trie — префиксное дерево для строк из 'a'..'z'.
type Trie struct {
	next [26]*Trie
	end  bool
}

func (t *Trie) Insert(w string) {
	for i := range len(w) {
		c := w[i] - 'a'
		if t.next[c] == nil {
			t.next[c] = &Trie{}
		}
		t = t.next[c]
	}
	t.end = true
}

func (t *Trie) find(p string) *Trie {
	for i := range len(p) {
		if t = t.next[p[i]-'a']; t == nil {
			return nil
		}
	}
	return t
}

func (t *Trie) Search(w string) bool     { n := t.find(w); return n != nil && n.end }
func (t *Trie) StartsWith(p string) bool { return t.find(p) != nil }
```

</details>

<a id="tpl-13"></a>
<details>
<summary><b>13. Backtracking</b> — перебор с откатом</summary>

```go
// subsets — все подмножества.
func subsets(nums []int) [][]int {
	var res [][]int
	var path []int
	var dfs func(i int)
	dfs = func(i int) {
		if i == len(nums) {
			res = append(res, slices.Clone(path)) // без Clone ответы делят один массив
			return
		}
		dfs(i + 1) // не берём nums[i]
		path = append(path, nums[i])
		dfs(i + 1) // берём
		path = path[:len(path)-1]
	}
	dfs(0)
	return res
}
```

</details>

<a id="tpl-14"></a>
<details>
<summary><b>14. Связный список</b> — разворот, быстрый и медленный указатели</summary>

```go
type ListNode struct {
	Val  int
	Next *ListNode
}

func reverseList(head *ListNode) *ListNode {
	var prev *ListNode
	for cur := head; cur != nil; {
		next := cur.Next
		cur.Next = prev
		prev, cur = cur, next
	}
	return prev
}

// middle — середина списка (при чётной длине — вторая из двух).
func middle(head *ListNode) *ListNode {
	slow, fast := head, head
	for fast != nil && fast.Next != nil {
		slow, fast = slow.Next, fast.Next.Next
	}
	return slow
}
```

</details>

<a id="tpl-15"></a>
<details>
<summary><b>15. Дерево</b> — рекурсивный DFS и BFS по уровням</summary>

```go
type TreeNode struct {
	Val         int
	Left, Right *TreeNode
}

func maxDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}
	return 1 + max(maxDepth(root.Left), maxDepth(root.Right))
}

func levelOrder(root *TreeNode) [][]int {
	var res [][]int
	if root == nil {
		return res
	}
	q := []*TreeNode{root}
	for len(q) > 0 {
		n := len(q) // размер текущего уровня
		level := make([]int, 0, n)
		for i := 0; i < n; i++ {
			node := q[i]
			level = append(level, node.Val)
			if node.Left != nil {
				q = append(q, node.Left)
			}
			if node.Right != nil {
				q = append(q, node.Right)
			}
		}
		q = q[n:]
		res = append(res, level)
	}
	return res
}
```

</details>

<a id="tpl-16"></a>
<details>
<summary><b>16. Динамическое программирование</b> — одномерное и двумерное</summary>

```go
// coinChange — минимум монет для суммы amount или -1.
func coinChange(coins []int, amount int) int {
	dp := make([]int, amount+1) // dp[s] — минимум монет для суммы s
	for s := 1; s <= amount; s++ {
		dp[s] = math.MaxInt
		for _, c := range coins {
			if c <= s && dp[s-c] != math.MaxInt {
				dp[s] = min(dp[s], dp[s-c]+1)
			}
		}
	}
	if dp[amount] == math.MaxInt {
		return -1
	}
	return dp[amount]
}

// lcs — длина наибольшей общей подпоследовательности.
func lcs(a, b string) int {
	dp := make([][]int, len(a)+1)
	for i := range dp {
		dp[i] = make([]int, len(b)+1)
	}
	for i := 1; i <= len(a); i++ {
		for j := 1; j <= len(b); j++ {
			if a[i-1] == b[j-1] {
				dp[i][j] = dp[i-1][j-1] + 1
			} else {
				dp[i][j] = max(dp[i-1][j], dp[i][j-1])
			}
		}
	}
	return dp[len(a)][len(b)]
}
```

Схема: что хранит `dp[i]` → переход → база → порядок обхода → где ответ.

</details>

<a id="tpl-17"></a>
<details>
<summary><b>17. Интервалы</b> — сортировка и слияние</summary>

```go
// mergeIntervals — слияние пересекающихся отрезков.
func mergeIntervals(iv [][]int) [][]int {
	slices.SortFunc(iv, func(a, b []int) int { return cmp.Compare(a[0], b[0]) })
	var res [][]int
	for _, cur := range iv {
		if n := len(res); n > 0 && cur[0] <= res[n-1][1] {
			res[n-1][1] = max(res[n-1][1], cur[1])
		} else {
			res = append(res, []int{cur[0], cur[1]}) // копия: не портим вход
		}
	}
	return res
}
```

</details>

<a id="tpl-18"></a>
<details>
<summary><b>18. LRU-кэш</b> — <code>container/list</code> + map</summary>

```go
type entry struct{ key, val int }

// LRUCache — кэш на двусвязном списке и map.
type LRUCache struct {
	cap   int
	ll    *list.List // в начале — самые свежие
	items map[int]*list.Element
}

func NewLRU(capacity int) *LRUCache {
	return &LRUCache{cap: capacity, ll: list.New(), items: make(map[int]*list.Element)}
}

func (c *LRUCache) Get(key int) int {
	el, ok := c.items[key]
	if !ok {
		return -1
	}
	c.ll.MoveToFront(el)
	return el.Value.(*entry).val
}

func (c *LRUCache) Put(key, val int) {
	if el, ok := c.items[key]; ok {
		el.Value.(*entry).val = val
		c.ll.MoveToFront(el)
		return
	}
	c.items[key] = c.ll.PushFront(&entry{key, val})
	if c.ll.Len() > c.cap {
		last := c.ll.Back()
		c.ll.Remove(last)
		delete(c.items, last.Value.(*entry).key)
	}
}
```

На LeetCode конструктор называется `Constructor(capacity int) LRUCache`.

</details>

---

<a id="tasks"></a>
## ✅ Задачи по паттернам

<a id="t-arrays"></a>
### 1. Массивы и хеширование

- [ ] ★ 🟢 [Two Sum](https://leetcode.com/problems/two-sum/) 🔥
- [ ] ★ 🟢 [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- [ ] ★ 🟢 [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- [ ] ★ 🟡 [Group Anagrams](https://leetcode.com/problems/group-anagrams/) 🔥
- [ ] ★ 🟡 [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) 🔥
- [ ] ★ 🟢 [Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/) 🔥
- [ ] 🟡 [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
- [ ] 🟡 [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Two Sum** — map «значение → индекс», один проход, O(n)
- **Contains Duplicate** — множество `map[int]struct{}`
- **Valid Anagram** — счётчик `[26]int`
- **Group Anagrams** — ключ — счётчик `[26]byte` (массив сравним, годится в ключ map)
- **Top K Frequent Elements** — частоты в map + bucket sort по частоте, O(n)
- **Intersection of Two Arrays II** — счётчик по одному массиву, проход по второму
- **Product of Array Except Self** — произведения слева и справа, без деления
- **Longest Consecutive Sequence** — множество; считаем только от x, у которого нет x−1

</details>

<a id="t-two-pointers"></a>
### 2. Два указателя

Шаблоны: [3. Два указателя](#tpl-3)

- [ ] ★ 🟢 [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [ ] ★ 🟢 [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
- [ ] ★ 🟡 [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- [ ] ★ 🟡 [3Sum](https://leetcode.com/problems/3sum/)
- [ ] 🟡 [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- [ ] ★ 🔴 [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) 🔥

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Valid Palindrome** — указатели с двух концов, пропускаем не буквы и не цифры
- **Merge Sorted Array** — заполняем с конца
- **Two Sum II - Input Array Is Sorted** — сумма больше цели — двигаем правый, меньше — левый
- **3Sum** — сортировка, фиксируем первый, дальше два указателя; пропускаем дубли
- **Container With Most Water** — всегда двигаем меньшую стенку
- **Trapping Rain Water** — два указателя и максимумы слева и справа, O(1) памяти

</details>

<a id="t-window"></a>
### 3. Скользящее окно

Шаблоны: [4. Скользящее окно](#tpl-4)

- [ ] ★ 🟢 [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- [ ] ★ 🟡 [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [ ] 🟡 [Permutation in String](https://leetcode.com/problems/permutation-in-string/)
- [ ] 🔴 [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [ ] 🔴 [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Best Time to Buy and Sell Stock** — минимум цены слева + лучшая разница
- **Longest Substring Without Repeating Characters** — окно + последняя позиция каждого символа
- **Permutation in String** — окно фиксированной длины, сравниваем счётчики `[26]int`
- **Minimum Window Substring** — расширяем до покрытия, сужаем, пока покрыто
- **Sliding Window Maximum** — монотонная дека индексов

</details>

<a id="t-prefix"></a>
### 4. Префиксные суммы

Шаблоны: [5. Префиксные суммы + map](#tpl-5)

- [ ] ★ 🟢 [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)
- [ ] ★ 🟡 [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
- [ ] 🟡 [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Range Sum Query - Immutable** — `pref[i+1] = pref[i] + a[i]`, сумма отрезка — `pref[r+1] − pref[l]`
- **Subarray Sum Equals K** — map «префиксная сумма → сколько раз встречалась»
- **Continuous Subarray Sum** — map «остаток префикса по модулю k → первый индекс»

</details>

<a id="t-strings"></a>
### 5. Строки

- [ ] ★ 🟡 [String Compression](https://leetcode.com/problems/string-compression/) 🔥
- [ ] ★ 🟢 [Summary Ranges](https://leetcode.com/problems/summary-ranges/) 🔥
- [ ] 🟡 [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)
- [ ] 🟢 [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **String Compression** — RLE на месте: указатель чтения и указатель записи
- **Summary Ranges** — сворачиваем подряд идущие числа в диапазоны `a->b`
- **Reverse Words in a String** — `strings.Fields` + разворот слайса
- **Valid Palindrome II** — при первом несовпадении пробуем пропустить символ слева или справа

</details>

<a id="t-stack"></a>
### 6. Стек и монотонный стек

Шаблоны: [6. Монотонный стек](#tpl-6)

- [ ] ★ 🟢 [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) 🔥
- [ ] ★ 🟡 [Min Stack](https://leetcode.com/problems/min-stack/)
- [ ] ★ 🟡 [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
- [ ] 🔴 [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Valid Parentheses** — стек открывающих, map «закрывающая → открывающая»
- **Min Stack** — второй стек с текущими минимумами
- **Daily Temperatures** — монотонно убывающий стек индексов
- **Largest Rectangle in Histogram** — монотонный стек: ближайший меньший слева и справа

</details>

<a id="t-binary-search"></a>
### 7. Бинарный поиск

Шаблоны: [2. Бинарный поиск](#tpl-2)

- [ ] ★ 🟢 [Binary Search](https://leetcode.com/problems/binary-search/) 🔥
- [ ] ★ 🟡 [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- [ ] ★ 🟡 [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
- [ ] ★ 🟡 [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [ ] 🟡 [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
- [ ] 🟡 [Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Binary Search** — `mid := lo + (hi-lo)/2`, следим за границами
- **Find First and Last Position of Element in Sorted Array** — два lower bound: для x и для x+1
- **Koko Eating Bananas** — бинпоиск по ответу: успеет ли со скоростью v за h часов
- **Search in Rotated Sorted Array** — одна из половин всегда отсортирована
- **Find Minimum in Rotated Sorted Array** — сравниваем mid с правым краем
- **Time Based Key-Value Store** — map ключ → слайс (время, значение), бинпоиск по времени

</details>

<a id="t-linked-list"></a>
### 8. Связные списки

Шаблоны: [14. Связный список](#tpl-14) · [18. LRU-кэш](#tpl-18)

- [ ] ★ 🟢 [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) 🔥
- [ ] ★ 🟢 [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- [ ] ★ 🟢 [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
- [ ] 🟡 [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- [ ] 🟡 [Reorder List](https://leetcode.com/problems/reorder-list/)
- [ ] ★ 🟡 [LRU Cache](https://leetcode.com/problems/lru-cache/) 🔥
- [ ] 🔴 [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Reverse Linked List** — prev, cur, next; потом то же рекурсивно
- **Merge Two Sorted Lists** — фиктивная голова (dummy)
- **Linked List Cycle** — быстрый и медленный указатели
- **Remove Nth Node From End of List** — второй указатель с отставанием n + dummy
- **Reorder List** — середина → разворот второй половины → слияние
- **LRU Cache** — `container/list` + map «ключ → элемент списка»
- **Merge k Sorted Lists** — куча из голов списков или попарное слияние

</details>

<a id="t-trees"></a>
### 9. Деревья

Шаблоны: [15. Дерево: DFS и BFS](#tpl-15)

- [ ] ★ 🟢 [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [ ] ★ 🟢 [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- [ ] 🟢 [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
- [ ] ★ 🟡 [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- [ ] 🟡 [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)
- [ ] ★ 🟡 [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
- [ ] ★ 🟡 [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
- [ ] 🟡 [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- [ ] 🔴 [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Maximum Depth of Binary Tree** — `1 + max(левое, правое)`
- **Invert Binary Tree** — рекурсивно меняем детей местами
- **Diameter of Binary Tree** — высота поддеревьев + глобальный максимум `left + right`
- **Binary Tree Level Order Traversal** — BFS: обрабатываем уровень целиком (`len(q)` в начале уровня)
- **Binary Tree Right Side View** — BFS: последний узел каждого уровня
- **Validate Binary Search Tree** — рекурсия с границами (min, max)
- **Lowest Common Ancestor of a Binary Search Tree** — оба меньше — влево, оба больше — вправо, иначе текущий
- **Lowest Common Ancestor of a Binary Tree** — нашли в обоих поддеревьях — ответ текущий узел
- **Binary Tree Maximum Path Sum** — вклад узла — `val + max(0, лучший потомок)`, ответ — глобальный максимум

</details>

<a id="t-heap"></a>
### 10. Куча, top-K

Шаблоны: [9. Куча: top-K](#tpl-9)

- [ ] ★ 🟢 [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
- [ ] ★ 🟡 [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- [ ] 🟡 [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
- [ ] 🟡 [Task Scheduler](https://leetcode.com/problems/task-scheduler/)
- [ ] 🔴 [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Kth Largest Element in a Stream** — min-куча размера k
- **Kth Largest Element in an Array** — min-куча размера k или quickselect
- **K Closest Points to Origin** — max-куча размера k по расстоянию
- **Task Scheduler** — формула по максимальной частоте или куча
- **Find Median from Data Stream** — две кучи: max слева, min справа, балансируем размеры

</details>

<a id="t-backtracking"></a>
### 11. Рекурсия и backtracking

Шаблоны: [13. Backtracking](#tpl-13)

- [ ] ★ 🟡 [Subsets](https://leetcode.com/problems/subsets/)
- [ ] ★ 🟡 [Permutations](https://leetcode.com/problems/permutations/)
- [ ] ★ 🟡 [Combination Sum](https://leetcode.com/problems/combination-sum/)
- [ ] ★ 🟡 [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
- [ ] 🟡 [Word Search](https://leetcode.com/problems/word-search/)
- [ ] 🔴 [N-Queens](https://leetcode.com/problems/n-queens/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Subsets** — взять или не взять; перед сохранением копируем path
- **Permutations** — `used[]` + path
- **Combination Sum** — элемент можно брать повторно — рекурсия с тем же индексом
- **Generate Parentheses** — открыть, пока `open < n`; закрыть, пока `close < open`
- **Word Search** — DFS по сетке, временно помечаем клетку посещённой
- **N-Queens** — множества занятых столбцов и двух диагоналей

</details>

<a id="t-graphs"></a>
### 12. Графы

Шаблоны: [7. BFS по сетке](#tpl-7) · [8. Топологическая сортировка](#tpl-8) · [10. Dijkstra](#tpl-10) · [11. Union-Find](#tpl-11)

- [ ] ★ 🟡 [Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [ ] 🟡 [Clone Graph](https://leetcode.com/problems/clone-graph/)
- [ ] ★ 🟡 [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
- [ ] ★ 🟡 [Course Schedule](https://leetcode.com/problems/course-schedule/)
- [ ] 🟡 [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
- [ ] 🟡 [Number of Provinces](https://leetcode.com/problems/number-of-provinces/)
- [ ] 🟡 [Redundant Connection](https://leetcode.com/problems/redundant-connection/)
- [ ] ★ 🟡 [Network Delay Time](https://leetcode.com/problems/network-delay-time/)
- [ ] 🔴 [Word Ladder](https://leetcode.com/problems/word-ladder/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Number of Islands** — DFS или BFS по сетке, заливка
- **Clone Graph** — map «старый узел → новый» + DFS
- **Rotting Oranges** — BFS сразу из всех источников
- **Course Schedule** — поиск цикла: топосорт Кана или DFS с тремя цветами
- **Course Schedule II** — порядок из топологической сортировки
- **Number of Provinces** — DFS или Union-Find
- **Redundant Connection** — Union-Find: ребро, соединяющее уже связанные вершины
- **Network Delay Time** — Dijkstra на `container/heap`
- **Word Ladder** — BFS по словам, соседи — замена одной буквы

</details>

<a id="t-intervals"></a>
### 13. Интервалы

Шаблоны: [17. Интервалы](#tpl-17)

- [ ] ★ 🟡 [Merge Intervals](https://leetcode.com/problems/merge-intervals/) 🔥
- [ ] 🟡 [Insert Interval](https://leetcode.com/problems/insert-interval/)
- [ ] 🟡 [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)
- [ ] 🟡 [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Merge Intervals** — сортировка по началу, сливаем с последним в ответе
- **Insert Interval** — три фазы: до, пересечение, после
- **Non-overlapping Intervals** — жадно по концу интервала
- **Minimum Number of Arrows to Burst Balloons** — сортировка по концу

</details>

<a id="t-greedy"></a>
### 14. Жадные алгоритмы

- [ ] ★ 🟡 [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- [ ] ★ 🟡 [Jump Game](https://leetcode.com/problems/jump-game/)
- [ ] 🟡 [Jump Game II](https://leetcode.com/problems/jump-game-ii/)
- [ ] 🟡 [Gas Station](https://leetcode.com/problems/gas-station/)
- [ ] 🟡 [Partition Labels](https://leetcode.com/problems/partition-labels/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Maximum Subarray** — Кадане: `cur = max(x, cur+x)`
- **Jump Game** — храним максимальную достижимую позицию
- **Jump Game II** — BFS по «уровням» достижимости
- **Gas Station** — если бензина в сумме хватает, старт — после последнего провала
- **Partition Labels** — последнее вхождение каждого символа

</details>

<a id="t-trie"></a>
### 15. Trie ⭐

Шаблоны: [12. Trie](#tpl-12)

- [ ] 🟡 [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
- [ ] 🟡 [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Implement Trie (Prefix Tree)** — узел: `[26]*node` + флаг конца слова
- **Design Add and Search Words Data Structure** — DFS по trie, `.` — перебор всех детей

</details>

<a id="t-dp"></a>
### 16. Динамическое программирование

Шаблоны: [16. Динамическое программирование](#tpl-16)

- [ ] ★ 🟢 [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [ ] ★ 🟡 [House Robber](https://leetcode.com/problems/house-robber/)
- [ ] ★ 🟡 [Coin Change](https://leetcode.com/problems/coin-change/)
- [ ] ★ 🟡 [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- [ ] 🟡 [Word Break](https://leetcode.com/problems/word-break/)
- [ ] 🟡 [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)
- [ ] ★ 🟡 [Unique Paths](https://leetcode.com/problems/unique-paths/)
- [ ] ★ 🟡 [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
- [ ] 🟡 [Edit Distance](https://leetcode.com/problems/edit-distance/)
- [ ] ★ 🟡 [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
- [ ] 🟡 [Coin Change II](https://leetcode.com/problems/coin-change-ii/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Climbing Stairs** — `dp[i] = dp[i−1] + dp[i−2]`, хватит двух переменных
- **House Robber** — `dp[i] = max(dp[i−1], dp[i−2] + a[i])`
- **Coin Change** — `dp[s] = min(dp[s−coin] + 1)`
- **Longest Increasing Subsequence** — O(n²) DP, потом O(n log n) с бинпоиском
- **Word Break** — `dp[i]` — можно ли разбить префикс длины i
- **Partition Equal Subset Sum** — рюкзак 0/1 на сумму/2
- **Unique Paths** — `dp[i][j] = сверху + слева`
- **Longest Common Subsequence** — совпали — диагональ + 1, иначе max(сверху, слева)
- **Edit Distance** — минимум из трёх операций + 1
- **Longest Palindromic Substring** — расширение от центра, O(n²)
- **Coin Change II** — число способов: цикл по монетам снаружи

</details>

<a id="t-bits-math"></a>
### 17. Биты, математика, матрицы

- [ ] ★ 🟢 [Single Number](https://leetcode.com/problems/single-number/)
- [ ] 🟢 [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)
- [ ] 🟢 [Missing Number](https://leetcode.com/problems/missing-number/)
- [ ] 🟡 [Pow(x, n)](https://leetcode.com/problems/powx-n/)
- [ ] 🟡 [Rotate Image](https://leetcode.com/problems/rotate-image/)
- [ ] ★ 🟡 [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

<details>
<summary>💡 Подсказки — открывай, если застрял или для сверки</summary>

- **Single Number** — XOR всех элементов
- **Number of 1 Bits** — `n &= n-1` или `bits.OnesCount`
- **Missing Number** — XOR индексов и значений или сумма
- **Pow(x, n)** — быстрое возведение в степень, отрицательная степень
- **Rotate Image** — транспонирование + разворот строк
- **Spiral Matrix** — четыре границы, сужаем после каждого прохода

</details>
