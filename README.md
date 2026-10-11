# HW1 «Фотолаборатория»

## Установка и проверка

```bash
pip install -r requirements.txt
pytest tests -q
```

## Финальные команды

### Гамма
```bash
python photolab.py gamma data/dark.jpg --gamma 0.5 -o out/dark_g05.jpg --hist out/dark_g05_hist.png
python photolab.py gamma data/dark.jpg --gamma 2 -o out/dark_g2.jpg --hist out/dark_g2_hist.png
```

### Баланс белого
```bash
python photolab.py wb data/bright.jpg --method grey-world -o out/bright_gw.jpg --hist out/bright_gw_hist.png
python photolab.py wb data/bright.jpg --method white-patch -o out/bright_wp.jpg --hist out/bright_wp_hist.png
```

### CLAHE
```bash
python photolab.py clahe data/dark.jpg --clip 2 --tiles 8 -o out/dark_clahe.jpg --compare out/dark_cmp.jpg --hist out/dark_clahe_hist.png
```

### Хромакей
```bash
python photolab.py chromakey data/object.jpg --bg data/bg.jpg --lo 15,60,10 --hi 29,200,255 --open 2 --close 9 --feather 1.0 -o out/object_on_bg.jpg --mask out/object_mask.png
```

### Поворот
```bash
python photolab.py rotate data/poster.jpg --deg 30 -o out/poster_rot30.jpg
```

### Масштабирование
```bash
python photolab.py resize data/text.jpg --scale 0.25 --method area --report -o out/text_area.jpg
python photolab.py resize data/text.jpg --scale 0.25 --method blur -o out/text_blur.jpg
python photolab.py resize data/text.jpg --scale 0.25 --method naive -o out/text_naive.jpg
```

### Выпрямление перспективы
```bash
python photolab.py rectify data/poster.jpg --corners 412.5,302.5,1150.0,297.5,1452.5,1065.0,100.0,1057.5 --aspect 0.707 -o out/poster_rect.jpg
```

### Контактный лист
```bash
python photolab.py sheet out/dark_g05.jpg out/dark_g2.jpg out/bright_gw.jpg out/bright_wp.jpg out/dark_clahe.jpg out/object_on_bg.jpg out/poster_rot30.jpg out/text_area.jpg out/poster_rect.jpg --cols 3 -o out/sheet.jpg
```

## Проверка на данных курса

```bash
python photolab.py chromakey data/ball-lamp.jpg --bg data/road-cam.jpg --lo 140,121,40 --hi 168,230,255 -o out/course_ck.jpg --mask out/course_ck_mask.png

python photolab.py resize data/iu-building.jpg --scale 0.25 --method area --report -o out/course_small.jpg

python photolab.py rectify data/poster-angle.jpg --corners 560,330,1250,220,1290,1010,600,840 --size 640x905 -o out/course_front640.jpg
```

Метрики проверочных прогонов приведены в `REPORT.md`.

## Структура

- `photolab.py` — реализация команд.
- `data/` — входные изображения.
- `out/` — результаты финальных команд.
- `REPORT.md` — отчёт с измерениями и выводами.
- `tests/` — автотесты.
- `requirements.txt` — зависимости.
