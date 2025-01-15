# Первый пример
# открываем файл
f = open('27_B_5__4uxkw.txt')
s = f.readline() #мусор в виде xy в начале файла
kolvo_klasterov = int(input('Введите кол-во кластеров: '))
kolvo_zvezd = int(input('Введите кол-во звёзд: '))
a = [[] for i in range(kolvo_klasterov)]
for tret in range(kolvo_zvezd):
    s = f.readline().replace(',', '.') # если в файле 3,5 а не 3.5
    xy = list(map(float, s.split()))
    if xy:
        if xy[0] > 10:
            a[0].append(xy)
        elif xy[0] > 6.5:
            a[1].append(xy)
        elif xy[1] < -3:
            a[2].append(xy)
        else:
            a[3].append(xy)
# Раскидали звезды по спискам в зависимости от их координат.
# Делаем тупой перебор, как говорится.
# Нужно следить за тем, что просят. Центроид - мин значение, Перифероид - макс.
sx=sy=0
for one in range(kolvo_klaserov): # перебираем кластеры
    mn = 10000000000000000000000 # устанавливаем максимум(минимум если перифероид)
    for two in range(len(a[one])): # берем звезду для сравнения в кластере
        x1, y1 = a[one][two] # координаты звезды (главная)
        ls = 0 # переменная для длины
        for three in range(len(a[one])): # перебираем остальные для сравнения с главной
            x2, y2 = a[one][three] # координаты остальных(по одному естественно)
            ls += ((x2-x1)**2 + (y2-y1)**2)**0.5 # формула для расстояния(расстояние до каждой из звезд мы складываем)
        if ls < mn: # проверка на минимум
            mn = ls
            t = a[one][two]
    sx += t[0] # х каждого центроида
    sy += t[1] # y каждого центроида
print(int((sx/kolvo_klaserov)*100), int((sy/kolvo_klaserov)*100))
