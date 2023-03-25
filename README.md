# Описание метода getItem(String source):
Данный метод возвращает ItemStack, основанный на конфигурации, в котором могут быть заданы любые свойства элемента.

* Метод `getItem(String source)` принимает строковое значение `source`, которое используется для определения пути до элемента в конфигурационном файле items.yml. Путь строится как `items.[source].[параметр]`. Значения всех параметров элемента определяются в файле `items.yml`. Если какой-то параметр не указан, используются значения по умолчанию для соответствующего типа элемента.
* Метод `getItems()` Возвращает `List<ItemStack>`, в котором содержится все предметы из конфигурационного файла. Если какой-то параметр не указан, используются значения по умолчанию для соответствующего типа элемента.

Список всех поддерживаемых параметров:

# Обязательные:
* `material`: тип материала, из которого сделан элемент. Обязательный параметр. Возможные значения можно посмотреть в документации по Material в Spigot. (https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html)
# Необязательные:
* `amount`: количество элементов в ItemStack. По умолчанию равен 1.
* `name`: отображаемое имя элемента. По умолчанию пусто.
* `lore`: описание элемента. По умолчанию пусто.
* `unbreakable`: указывает, может ли элемент быть сломан в игре. По умолчанию `false`.
* `custommodeldata`: определяет, какая модель будет использоваться для элемента. По умолчанию 0.
* `flags`: список флагов, которые определяют, какие свойства элемента могут быть изменены в игре. По умолчанию пусто. (https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/inventory/ItemFlag.html)
* `enchantments`: список зачарований, которые будут добавлены к элементу. Каждое зачарование задается как `имя_зачарования;уровень`. По умолчанию пусто. (https://hub.spigotmc.org/javadocs/spigot/org/bukkit/enchantments/Enchantment.html)
* `tags`: список пользовательских тегов, которые будут добавлены к элементу. Каждый тег задается как `имя_тега;значение`. По умолчанию пусто.
* `damage`: насколько едениц поврежден предмет, возможно нанести даную мета-дату только на предмет имеющий прочность.
* `color`: цвет элемента, если это кожаная броня, зелье или ведро с тропической рыбой. По умолчанию белый. (https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Color.html)
* `title`: заголовок книги, если это книга. По умолчанию пусто.
* `author`: автор книги, если это книга. По умолчанию пусто.
* `generation`: поколение книги, если это книга. Возможные значения: `ORIGINAL, COPY_OF_ORIGINAL, COPY_OF_COPY, TATTERED`. По умолчанию ORIGINAL.
* `pages`: список страниц книги, если это книга. По умолчанию пусто.
* `potioneffects`: список эффектов зелья, если это зелье. Каждый эффект задается как `имя_эффекта;уровень;время_действия`.
* `value`: base64 айди текстуры головы, налаживает текстуру на голову. Если материал равен `PLAYER_HEAD`
## Примеры конфигурации
Примеры конфигурации предметов, которые могут быть использованы с методом getItem, приведены ниже.
```yaml
items:
  my_sword:
    material: DIAMOND_SWORD
    amount: 1
    name: "&6Мой меч"
    lore:
      - "&eПрочный и острый"
      - "&cНе падайте в бою"
    unbreakable: true
    custommodeldata: 123
    flags:
      - "HIDE_ENCHANTS"
      - "HIDE_ATTRIBUTES"
    enchantments:
      - "DAMAGE_ALL;5"
      - "DURABILITY;3"
    tags:
      - "my_custom_tag;hello_world"
  my_armor:
    material: LEATHER_CHESTPLATE
    amount: 1
    color: "255;255;0"
  my_book:
    material: WRITTEN_BOOK
    amount: 1
    title: "&aМоя книга"
    author: "Power_Lands"
    generation: ORIGINAL
    pages:
      - "&cСтраница 1"
      - "&eСтраница 2"
  my_potion:
    material: POTION
    amount: 1
    color: "0;255;0"
    potioneffects:
      - "SPEED;2;60"
      - "JUMP;2;60"
  my_tropical_fish_bucket:
    material: TROPICAL_FISH_BUCKET
    amount: 1
    dyecolor: YELLOW
    pattern: "BRINELY"
    patterncolor: GREEN
  my_spawn_egg:
    material: SPAWN_EGG
    amount: 1
    eggentitytype: ZOMBIE
  my_banner:
    material: BLACK_BANNER
    amount: 1
    bannerbasecolor: YELLOW
    bannerpatterns:
      - "RED;STRIPE_BOTTOM"
      - "BLUE;STRIPE_CENTER"
  my_compass:
    material: COMPASS
    amount: 1
    lodestone: "0;0;0"
  my_custom_head:
    material: PLAYER_HEAD
    value: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvOWJlMzA1NDM2NWEyNDNkMmU5Yjc3NDE0ODJhMWY0MzVkYWVkNDM4MjliODk2MWRkYzQxMjZhODQ3MDYwYWQ0MiJ9fX0=
```
 Примечание: это только пример и может не работать в вашей конфигурации, так как зависит от многих факторов. Вы должны настроить конфигурационный файл в соответствии со своими потребностями и требованиями.
# Пример получения предмета из конфига
```java
Items items = new Items(my_plugin, "items.yml");
ItemStack stack = items.getItem("my_custom_head");
//Получаем готовый к использыванию предмет `stack`
```

# Вывод
Метод `getItem` предоставляет удобный способ создания предметов на основе предустановленной конфигурации. Он может быть использован в различных плагинах, где требуется создание предметов с определенными свойствами.
