# Passive Tree Planner

A POE1Fixer plugin. It shows a Path of Building build on the game's own passive skill tree:
which points to take next, numbered in order, and which points you have that the build does not
(to refund). Free for every licence key.

*Русская версия — ниже.*

## Install

In POE1Fixer (version 38 or newer): the **Plugins** tab, **Catalog**, **Passive Tree Planner**,
**Install**. It starts at once. Its settings are in its page's **Plugin settings** tab.

## What you see

Open the passive tree in the game (default key **P**). On top of it:

- **green rings**: points the build has and you have not taken yet;
- **step numbers** 1, 2, 3 … on the next points to take; **step 1** (the point to take now) is
  drawn in a bright colour with a thicker ring;
- **red rings**: points you have taken that the build does not have (refund them);
- **orange rings**: masteries you have taken with another effect than the build's;
- **lines** between linked points of the build, curved along an orbit where the game draws an arc;
- the **ascendancy** the same way, while its tree is shown;
- a **summary** at the top left: the build and its tree, how many points to take and to refund,
  your free points, and the next objective with its cost (the ascendancy's once the main tree is
  done);
- point at a ring to see the point's name, what to do with it, its step, the objective it leads to
  and, for a mastery, the effect the build wants.

Nothing is drawn while the passive tree is closed.

## Importing a build

In the app, open **Plugins → Passive Tree Planner → Plugin settings → Builds**, paste one of these
into the box and press **Import**:

- a **Path of Building export code** (PoB: *Import/Export Build → Generate*, then copy);
- a **pobb.in**, **pastebin.com** or **poe.ninja** build link (`https://pobb.in/…`,
  `https://pastebin.com/…`, `https://poe.ninja/pob/…`): the plugin downloads the code from that site;
- a **pathofexile.com passive tree link** (`https://www.pathofexile.com/passive-skill-tree/…`):
  decoded locally, nothing is downloaded.

**Long codes.** POE1Fixer passes up to 256 KB per paste into a plugin's panel (older versions only
16 KB, which cuts most endgame builds with their items). A code that arrives cut off is reported as
such. Links have no size limit: with an older POE1Fixer, share the build from Path of Building as a
pobb.in link (*Import/Export Build → Share → pobb.in*) and paste the link instead.

The build is saved (only its trees: points and masteries, never the code itself) and selected. A
build may hold several trees, as leveling builds do ("Lvl 01-30", "Lvl 31-60", …). With
**Automatic** and **Follow my level** on (the default), the plugin follows the tree whose title holds
your character's level (the narrowest range when several do). When none does, it follows the tree
that comes after the last range you have passed (an untitled "Endgame" tree, or the next range), and
below every range the earliest one. Builds without levels in their titles follow Path of Building's
active tree. Click a tree in the table to pick
it yourself. Builds can be renamed and deleted.

## How "next" is decided

The order is a real allocation order: every step touches what you already have or an earlier step.

1. The plugin starts from what you have: your allocated points and your class's start.
2. The **objectives** are the build's notables, keystones, jewel sockets and masteries you do not
   have yet.
3. It repeatedly picks the next objective it can reach, walking only through points the build
   wants, and puts the points of that path in walking order. With **Earlier trees first** on (the
   default), objectives the build's author already took in an **earlier tree** of the build come
   first, the earliest tree first; the rest follow. Within that, the objective **cheapest to reach**
   (the fewest points) wins; on a tie, the one needing fewer points that no earlier tree has.
   With the option off, the cheapest objective always comes first.
   A mastery can be taken once a notable of its group is allocated, and costs one point.
4. Then the build's remaining small points that can be reached.
5. Last, points that cannot be reached through the build's own points yet (the build passes through
   points you do not have, or through a point you should refund). They have no step number.

The Plan tab lists the next objectives with their cost in points, the masteries to pick with the
wanted effect, and what to refund.

## What it reads and what it sends

- It **reads game memory, read-only**, through the app, while you are in the game: the passive tree
  window's position and zoom, and your character's allocated passives, masteries, class, level and
  points. It never writes to the game and never presses keys.
- It uses the **network only** when you import a pobb.in / pastebin / poe.ninja link (one download
  of that build) or press **Update tree data** (one download of the official passive tree export,
  `github.com/grindinggear/skilltree-export`). Nothing about you, your account or your character is
  sent anywhere.
- It writes only to its own config folder: `settings.json`, `builds.json`, and `tree_official.json`
  after an update.

## Tree data

The plugin ships the official passive tree export. After a game patch that changes the tree, the
overlay says the tree data does not match the game: press **Update tree data** on the **Status** tab
to download the current export (a few MB). **Use bundled data** goes back to the shipped copy. The
Status tab also shows what the plugin reads, so a problem can be reported with its cause.

## Limits

- Only **applied** passives count. Points you planned in the game but have not applied yet are not
  seen.
- **Cluster-jewel** points are ignored (counted at import, not drawn).
- A Scion **Ascendant**'s "Path of the …" points, which open the main tree at another class's
  start, are not used for the order: it always starts from the Scion's own start and the points
  you have, so points reached only through such a start may be listed as not reachable yet.
- With an older POE1Fixer a code over 16 KB cannot be pasted whole (see *Importing a build*): update
  POE1Fixer or use a pobb.in link.
- Offsets inside game memory can change with a game patch. An `offsets.json` in the plugin's config
  folder can override them without a new build (the key names are in `data/offsets.json`).

---

# Планировщик дерева пассивок

Плагин POE1Fixer. Показывает билд из Path of Building прямо на дереве пассивных умений в игре: какие
очки брать дальше (с номерами по порядку) и какие из взятых очков в билде не нужны (их надо снять).
Бесплатен для любого ключа.

## Установка

В POE1Fixer (версия 38 или новее): вкладка **Плагины**, **Каталог**, **Passive Tree Planner**,
**Установить**. Плагин сразу запускается. Его настройки — на вкладке **Настройки плагина** его
страницы.

## Что видно

Откройте дерево пассивных умений в игре (по умолчанию клавиша **P**). Поверх него:

- **зелёные кольца** — очки, которые есть в билде, но ещё не взяты;
- **номера шагов** 1, 2, 3 … на следующих очках; **шаг 1** (очко, которое брать сейчас) выделен
  ярким цветом и толстым кольцом;
- **красные кольца** — взятые очки, которых нет в билде (их надо снять);
- **оранжевые кольца** — мастерства, взятые с другим эффектом, чем в билде;
- **линии** между связанными очками билда, дугой по орбите там, где дугу рисует сама игра;
- **Восхождение** — так же, пока его дерево на экране;
- **сводка** слева вверху: билд и его дерево, сколько очков взять и снять, ваши свободные очки и
  следующая цель с её ценой (цель Восхождения, когда основное дерево собрано);
- наведите курсор на кольцо — появится название очка, что с ним сделать, номер шага, к какой цели
  оно ведёт, а для мастерства — какой эффект нужен билду.

Пока дерево закрыто, ничего не рисуется.

## Импорт билда

В приложении откройте **Плагины → Планировщик дерева пассивок → настройки плагина → Билды**,
вставьте в поле одно из этого и нажмите **Импортировать**:

- **код экспорта Path of Building** (в PoB: *Import/Export Build → Generate*, затем скопировать);
- ссылку на билд **pobb.in**, **pastebin.com** или **poe.ninja** (`https://pobb.in/…`,
  `https://pastebin.com/…`, `https://poe.ninja/pob/…`) — плагин скачает код с этого сайта;
- **ссылку на дерево с pathofexile.com** (`https://www.pathofexile.com/passive-skill-tree/…`) —
  она расшифровывается на месте, ничего не скачивается.

**Длинный код.** POE1Fixer передаёт в панель плагина за одну вставку до 256 КБ (старые версии —
только 16 КБ, из-за чего обрезаются почти все эндгейм-билды с предметами). Если код пришёл
обрезанным, плагин об этом сообщает. У ссылок ограничения по размеру нет: в старой версии POE1Fixer
поделитесь билдом из Path of Building ссылкой pobb.in (*Import/Export Build → Share → pobb.in*) и
вставьте ссылку.

Билд сохраняется (только его деревья: очки и мастерства, сам код — никогда) и выбирается. В билде
может быть несколько деревьев, как в билдах для прокачки («Lvl 01-30», «Lvl 31-60», …). Если
включены **Автоматически** и **По моему уровню** (по умолчанию), плагин берёт дерево, в названии
которого есть уровень вашего персонажа (самый узкий диапазон, если таких несколько). Если такого
нет — дерево, идущее после последнего пройденного диапазона (например, «Endgame» без уровня или
следующий диапазон), а ниже всех диапазонов — самое раннее. Билды без уровней в названиях
деревьев используют активное дерево Path of Building. Щёлкните дерево в
таблице, чтобы выбрать его вручную. Билды можно переименовывать и удалять.

## Как выбирается «следующее»

Порядок — это настоящий порядок распределения: каждый шаг примыкает к уже взятому или к одному из
предыдущих шагов.

1. Плагин начинает с того, что у вас есть: взятые очки и стартовая точка вашего класса.
2. **Цели** — значимые и ключевые умения, гнёзда для самоцветов и мастерства из билда, которых у вас
   ещё нет.
3. Раз за разом выбирается следующая цель, до которой можно дойти только по очкам, нужным билду,
   и очки этого пути ставятся по порядку. Если включено **«Сначала цели прошлых деревьев»** (по
   умолчанию — да), первыми идут цели, которые автор билда взял уже в **более раннем дереве** билда,
   начиная с самого раннего дерева; остальные — после них. Внутри этого порядка побеждает цель, до
   которой **дешевле всего дойти** (меньше всего очков); при равенстве — та, где меньше очков,
   которых нет ни в одном раннем дереве. Если опция выключена, первой всегда идёт самая дешёвая
   цель. Мастерство можно взять, когда взято значимое умение его группы, и стоит оно одно очко.
4. Затем — остальные мелкие очки билда, до которых можно дойти.
5. В конце — очки, до которых пока не дойти по очкам самого билда (путь идёт через очки, которых у
   вас нет, или через очко, которое надо снять). Номеров у них нет.

На вкладке «План» — следующие цели с ценой в очках, какие мастерства выбрать (с нужным эффектом) и
что снять.

## Что плагин читает и что отправляет

- Он **читает память игры, только для чтения**, через приложение, пока вы в игре: положение и
  масштаб окна дерева, а также взятые очки, мастерства, класс, уровень и очки персонажа. Он ничего
  не пишет в игру и не нажимает клавиши.
- **Сеть** нужна только при импорте ссылки pobb.in / pastebin / poe.ninja (одна загрузка этого
  билда) и по кнопке **Обновить данные дерева** (одна загрузка официальной выгрузки дерева,
  `github.com/grindinggear/skilltree-export`). Ничего о вас, вашем аккаунте или персонаже никуда не
  отправляется.
- Пишет он только в свою папку настроек: `settings.json`, `builds.json` и после обновления —
  `tree_official.json`.

## Данные дерева

Вместе с плагином поставляется официальная выгрузка дерева. Если патч игры изменил дерево, оверлей
сообщит, что данные дерева не совпадают с игрой: нажмите **Обновить данные дерева** на вкладке
**Состояние**, чтобы скачать текущую выгрузку (несколько МБ). **Встроенные данные** возвращают копию
из комплекта плагина. На вкладке «Состояние» также видно, что именно читает плагин, — так о
проблеме можно сообщить вместе с её причиной.

## Ограничения

- Учитываются только **применённые** очки. Очки, запланированные в игре, но ещё не применённые, не
  видны.
- Очки **кластерных самоцветов** не учитываются (при импорте они подсчитываются, но не рисуются).
- Очки «Path of the …» восхождения **Ascendant** (класс Scion), которые открывают основное дерево
  от стартовой точки другого класса, для порядка не используются: он всегда строится от стартовой
  точки Scion и ваших взятых очков, поэтому очки, до которых можно дойти только от такой точки,
  могут числиться пока недостижимыми.
- В старой версии POE1Fixer код длиннее 16 КБ нельзя вставить целиком (см. «Импорт билда»):
  обновите POE1Fixer или используйте ссылку pobb.in.
- Смещения в памяти игры могут меняться с патчами. Файл `offsets.json` в папке настроек плагина
  может переопределить их без новой сборки (названия ключей — в `data/offsets.json`).
