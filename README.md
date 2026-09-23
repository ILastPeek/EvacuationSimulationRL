<h1 align="center">🏃 EvacuationSimulationRL</h1>

<p align="center">
  <b>Агент-ориентированная симуляция эвакуации людей из зданий<br>с обучением с подкреплением (Unity + ML-Agents)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Unity-2023.2.0f1-black?logo=unity" alt="Unity">
  <img src="https://img.shields.io/badge/ML--Agents-1.1.0-blue" alt="ML-Agents">
  <img src="https://img.shields.io/badge/PyTorch-2.2.1-ee4c2c?logo=pytorch" alt="PyTorch">
  <img src="https://img.shields.io/badge/Python-3.10-3776AB?logo=python" alt="Python">
  <img src="https://img.shields.io/badge/C%23-.NET-512BD4?logo=dotnet" alt="C#">
</p>

---

## 📖 О проекте

Агенты **не имеют глобальной карты здания** и обучаются находить выходы
только на основе локальных сенсорных данных. Это имитирует ограниченное
восприятие человека в условиях пожара или чрезвычайной ситуации.

> 🎯 **Цель проекта:** исследовать, как обучение с подкреплением справляется
> с задачей коллективной эвакуации в условиях частичной наблюдаемости.

---

## 🎬 Демонстрация

### Сцена симуляции

<p align="center">
  <img src="https://raw.githubusercontent.com/ILastPeek/EvacuationSimulationRL/main/40%20-%20frame.jpg" alt="Сцена симуляции" width="80%">
</p>

### Визуализация лучей восприятия

<p align="center">
  <img src="https://raw.githubusercontent.com/ILastPeek/EvacuationSimulationRL/main/image.png" alt="Лучи RayPerceptionSensor3D" width="80%">
</p>

<p align="center">
  <i>Агенты «видят» мир через 180° дугу лучей: стены, других агентов, двери и выходы.</i>
</p>

---

## 🛠 Стек

| Технология | Версия | Роль |
|---|---|---|
| **Unity** | 2023.2.0f1 | Среда симуляции |
| **ML-Agents** | 1.1.0 | Фреймворк RL |
| **PyTorch** | 2.2.1 | Обучение нейросети |
| **Python** | 3.10 | Backend обучения |
| **C#** | — | Логика агентов и среды |
| **TensorBoard** | — | Визуализация метрик |

---

## 🧠 Как это работает

### 👁 Локальное восприятие

Каждый агент «видит» мир только через `RayPerceptionSensor3D` —
**180° дуга с двухуровневым сканированием**. Лучи детектируют стены,
других агентов, выходы и двери. Низкие барьеры не блокируют обзор:
лучи проходят поверх них.

> Глобальная карта здания агенту **недоступна** — он учится искать выход
> по локальным сигналам, как человек в незнакомом помещении.

### 🎁 Система наград

| Событие | Награда |
|---|---|
| ✅ Достижение выхода | **+** |
| ❌ Столкновение со стеной | **−** |
| ❌ Столкновение с другим агентом | **−** |
| ⏱ Каждая секунда промедления | **−** |

Благодаря такой схеме агент учится не только находить выход,
но и делать это **быстро, не создавая давку**.

### 🌍 Динамическое окружение

- 🎲 Случайное размещение агентов в начале каждого эпизода
- 🚪 Открывающиеся и закрывающиеся двери
- 👥 Реалистичное взаимодействие агентов между собой

---

## 🏗 Архитектура

| Файл | Отвечает за |
|---|---|
| `Agent_Logic.cs` | Действия агента, сбор наблюдений, обработка коллизий |
| `LevelManager.cs` | Регистрация агентов, сброс эпизодов, расчёт наград |
| `AgentSettings.cs` | `ScriptableObject` с параметрами симуляции |
| `Door.cs` | Управление состоянием дверей (открыто / закрыто) |

---

## 📈 Обучение

Модель обучена через ML-Agents. Метрики (рост награды, длина эпизода,
доля успешных эвакуаций) визуализированы в TensorBoard.

<!-- Если есть график — раскомментируй и подставь путь
<p align="center">
  <img src="docs/training/training_progress.png" alt="Прогресс обучения" width="70%">
</p>
-->

---

## 🚀 Запуск

### Требования

- Unity **2023.2.0f1** (или совместимая)
- Python **3.10**
- ML-Agents Toolkit

### Установка

### Установка

```bash
git clone https://github.com/ILastPeek/EvacuationSimulationRL.git
cd EvacuationSimulationRL
```

1. Открой проект через **Unity Hub**.
2. Установи Python-зависимости: `pip install mlagents==1.1.0`
3. Запусти обучение: `mlagents-learn config/trainer_config.yaml --run-id=run1`
4. Открой сцену `Assets/Scenes/Main.unity` в Unity и нажми **Play**.

---

## 🎓 Контекст

Проект выполнен в рамках дипломной работы по теме **«Применение обучения с подкреплением в агент-ориентированном моделировании эвакуации людей из зданий»**.

Диплом защищён с **отличием**.

---

## 👤 Автор

**Емельянов Максим**

[![GitHub](https://img.shields.io/badge/GitHub-ILastPeek-181717?logo=github)](https://github.com/ILastPeek)
[![Telegram](https://img.shields.io/badge/Telegram-@LastPeek-26A5E4?logo=telegram)](https://t.me/LastPeek)
[![Email](https://img.shields.io/badge/Email-thelastpeek@gmail.com-EA4335?logo=gmail)](mailto:thelastpeek@gmail.com)

---

<p align="center">
  <i>Если проект оказался полезен — поставь ⭐ репозиторию!</i>
</p>
