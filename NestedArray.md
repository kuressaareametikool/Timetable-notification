# Building Nested Arrays in PHP (Laravel Example)

## Goal

Transform a flat list of timetable events into a grouped structure where lessons are organized by weekday.

---

## Input Data (Flat Structure)

```php
$content = [
    [
        'date' => '2026-01-26',
        'nameEt' => 'Matemaatika',
        'timeStart' => '08:30',
        'timeEnd' => '10:00',
    ],
    [
        'date' => '2026-01-26',
        'nameEt' => 'Füüsika',
        'timeStart' => '10:15',
        'timeEnd' => '11:45',
    ],
    [
        'date' => '2026-01-27',
        'nameEt' => 'Keemia',
        'timeStart' => '09:00',
        'timeEnd' => '10:30',
    ],
];
```

Each array element represents **one lesson**.

---

## Target Data Structure (Nested)

```php
$items = [
    'Esmaspäev' => [
        [
            'name' => 'Matemaatika',
            'start' => '08:30',
            'end' => '10:00',
        ],
        [
            'name' => 'Füüsika',
            'start' => '10:15',
            'end' => '11:45',
        ],
    ],
    'Teisipäev' => [
        [
            'name' => 'Keemia',
            'start' => '09:00',
            'end' => '10:30',
        ],
    ],
];
```

Structure:

```php
$items[DAY][] = LESSON_ARRAY
```

---

## Step 1: Initialize the Container

```php
$items = [];
```

Creates an empty array to store grouped lessons.

---

## Step 2: Loop Through Lessons

```php
foreach ($content as $item) {
    // process one lesson
}
```

---

## Step 3: Determine Group Key (Weekday)

```php
$date = Carbon::parse($item['date'])->locale('et');
$day = $date->dayName;
```

---

## Step 4: Append Lesson to Day

```php
$items[$day][] = [
    'name' => $item['nameEt'],
    'start' => $item['timeStart'],
    'end' => $item['timeEnd'],
];
```

If the day key does not exist, PHP creates it automatically.

---

## Result After Processing

```php
[
    'Esmaspäev' => [
        [ 'Matemaatika' ],
        [ 'Füüsika' ],
    ],
    'Teisipäev' => [
        [ 'Keemia' ],
    ],
]
```

---

## Equivalent Expanded Version

```php
if (!isset($items[$day])) {
    $items[$day] = [];
}

$items[$day][] = [
    'name' => $item['nameEt'],
    'start' => $item['timeStart'],
    'end' => $item['timeEnd'],
];
```

---

## Key Rules

* `=` assigns or replaces a value
* `[]` appends a value to an array
* Nested arrays represent grouped data
* Grouping key determines where data is stored

---

