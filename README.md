🚀 ELITE HUB - ПОЛНЫЙ ТУТОРИАЛ ДЛЯ НАЧИНАЮЩИХ
📚 ОГЛАВЛЕНИЕ

    Установка и базовое использование

    Создание окна

    Система вкладок

    Элементы управления

    Анимации и эффекты

    Практические примеры

    Советы и лучшие практики

1. УСТАНОВКА И БАЗОВОЕ ИСПОЛЬЗОВАНИЕ
🎯 ШАГ 1: КОПИРОВАНИЕ БИБЛИОТЕКИ
lua

-- Вставьте этот код в начало вашего скрипта
local EliteHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/your-repo/elite-hub/main/library.lua"))()

ИЛИ если вы используете локальную версию:
lua

-- Просто скопируйте весь код библиотеки в начало вашего скрипта
-- [Весь код Elite Hub который я предоставил ранее]

🎯 ШАГ 2: ПРОВЕРКА РАБОТОСПОСОБНОСТИ
lua

-- Простой тест для проверки
print("🚀 Elite Hub загружен!")
print("Доступные цвета:", EliteHub.Colors)
print("Доступные функции:", EliteHub.Tween, EliteHub.Notify)

2. СОЗДАНИЕ ОКНА
🎯 БАЗОВОЕ ОКНО
lua

-- Создание основного окна
local MyWindow = EliteHub:CreateWindow("Мое меню")

-- Создание кнопки для открытия окна
EliteHub:CreateOpenButton(MyWindow)

-- Показ уведомления о загрузке
EliteHub:Notify("Успех", "Меню загружено! 🎉", 3, "Success")

🎯 РАСШИРЕННЫЕ НАСТРОЙКИ ОКНА
lua

local AdvancedWindow = EliteHub:CreateWindow("Продвинутое меню")

-- Программное открытие окна
AdvancedWindow.Open()

-- Программное закрытие окна
AdvancedWindow.Close()

-- Проверка состояния окна
if AdvancedWindow.IsOpen() then
    print("Окно открыто")
else
    print("Окно закрыто")
end

-- Переключение состояния окна
AdvancedWindow.ToggleWindow()

3. СИСТЕМА ВКЛАДОК
🎯 СОЗДАНИЕ БАЗОВЫХ ВКЛАДОК
lua

local Window = EliteHub:CreateWindow("Многовадкадное меню")

-- Создание нескольких вкладок
local MainTab = EliteHub:CreateTab(Window, "Главная", "🏠")
local CombatTab = EliteHub:CreateTab(Window, "Бой", "⚔️")
local VisualTab = EliteHub:CreateTab(Window, "Визуалы", "👁️")
local SettingsTab = EliteHub:CreateTab(Window, "Настройки", "⚙️")

🎯 ПРОГРАММНОЕ ПЕРЕКЛЮЧЕНИЕ ВКЛАДОК
lua

-- Переключение на определенную вкладку
EliteHub:SwitchTab(Window, CombatTab)

-- Перебор всех вкладок
for i, tab in ipairs(Window.Tabs) do
    print("Вкладка " .. i .. ": " .. tab.Button.Text)
end

4. ЭЛЕМЕНТЫ УПРАВЛЕНИЯ
🎯 4.1 СЕКЦИИ (РАЗДЕЛИТЕЛИ)
lua

local Tab = EliteHub:CreateTab(Window, "Элементы", "🎛️")

-- Создание секций для группировки
local BasicSection = EliteHub:CreateSection(Tab, "Основные элементы")
local AdvancedSection = EliteHub:CreateSection(Tab, "Продвинутые элементы")
local SettingsSection = EliteHub:CreateSection(Tab, "Настройки")

🎯 4.2 КНОПКИ (BUTTONS)
lua

-- Простая кнопка
EliteHub:CreateButton(Tab, "Обычная кнопка", function()
    print("Кнопка нажата!")
    EliteHub:Notify("Кнопка", "Функция выполнена! ✅", 2, "Success")
end)

-- Кнопка с задержкой
EliteHub:CreateButton(Tab, "Кнопка с задержкой", function()
    EliteHub:Notify("Инфо", "Запуск через 3 секунды...", 2, "Info")
    wait(3)
    EliteHub:Notify("Успех", "Задача выполнена! 🎯", 2, "Success")
end)

-- Опасная кнопка
EliteHub:CreateButton(Tab, "Опасное действие", function()
    EliteHub:Notify("Внимание", "Выполняется опасная операция!", 3, "Danger")
end)

🎯 4.3 ПЕРЕКЛЮЧАТЕЛИ (TOGGLES)
lua

-- Базовый переключатель
local AimbotToggle = EliteHub:CreateToggle(Tab, "Аимбот", false, function(State)
    if State then
        EliteHub:Notify("Аимбот", "Функция включена 🎯", 2, "Success")
        -- Код включения аимбота
    else
        EliteHub:Notify("Аимбот", "Функция выключена", 2, "Info")
        -- Код выключения аимбота
    end
end)

-- Переключатель с автоматическим включением
local AutoFarmToggle = EliteHub:CreateToggle(Tab, "Авто-фарм", true, function(State)
    EliteHub:Notify("Авто-фарм", State and "Запущен 🌾" or "Остановлен", 2, "Info")
end)

-- Программное управление переключателем
AimbotToggle.Set(true)  -- Включить
AimbotToggle.Set(false) -- Выключить

local currentState = AimbotToggle.Get() -- Получить состояние

🎯 4.4 СЛАЙДЕРЫ (SLIDERS)
lua

-- Слайдер для настроек
local WalkSpeedSlider = EliteHub:CreateSlider(Tab, "Скорость ходьбы", 16, 200, 50, function(Value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
    EliteHub:Notify("Скорость", "Установлена: " .. Value, 1, "Info")
end)

-- Слайдер для визуальных настроек
local FOVSlider = EliteHub:CreateSlider(Tab, "Поле зрения", 70, 120, 80, function(Value)
    game.Workspace.CurrentCamera.FieldOfView = Value
end)

-- Программное управление слайдером
WalkSpeedSlider.Set(100) -- Установить значение
local currentSpeed = WalkSpeedSlider.Get() -- Получить текущее значение

5. АНИМАЦИИ И ЭФФЕКТЫ
🎯 5.1 КАСТОМНЫЕ АНИМАЦИИ
lua

-- Создание кастомной анимации для любого объекта
local MyFrame = Instance.new("Frame")
MyFrame.Size = UDim2.new(0, 100, 0, 100)
MyFrame.BackgroundColor3 = EliteHub.Colors.Accent

-- Анимация размера и позиции
EliteHub:Tween(MyFrame, {
    Size = UDim2.new(0, 200, 0, 200),
    Position = UDim2.new(0.5, -100, 0.5, -100),
    Rotation = 360
}, 1.0, Enum.EasingStyle.Bounce)

-- Разные стили анимации
EliteHub:Tween(MyFrame, {Size = UDim2.new(0, 150, 0, 150)}, 0.5, Enum.EasingStyle.Linear)
EliteHub:Tween(MyFrame, {Position = UDim2.new(0, 50, 0, 50)}, 0.5, Enum.EasingStyle.Quad)
EliteHub:Tween(MyFrame, {BackgroundTransparency = 0.5}, 0.5, Enum.EasingStyle.Circular)

🎯 5.2 ЭФФЕКТ ВОЛНЫ
lua

-- Эффект волны на кнопке
local TestButton = EliteHub:CreateButton(Tab, "Тест волны", function()
    -- Волна при клике (автоматически)
end)

-- Ручной вызов эффекта волны
EliteHub:WaveEffect(TestButton, EliteHub.Colors.Success)

-- Волна на разных элементах
EliteHub:WaveEffect(Window.MainFrame, EliteHub.Colors.Accent)

🎯 5.3 ЭФФЕКТ СВЕЧЕНИЯ
lua

-- Свечение при наведении (автоматически в элементах)

-- Ручное создание свечения
local SpecialButton = EliteHub:CreateButton(Tab, "Особая кнопка", function()
    EliteHub:GlowEffect(SpecialButton, EliteHub.Colors.Warning, 2.0)
end)

6. ПРАКТИЧЕСКИЕ ПРИМЕРЫ
🎯 ПРИМЕР 1: МЕНЮ ДЛЯ ИГРЫ
lua

-- Создание игрового меню
local GameMenu = EliteHub:CreateWindow("Game HUB v2.0")
EliteHub:CreateOpenButton(GameMenu)

-- Вкладки
local MainTab = EliteHub:CreateTab(GameMenu, "Главная", "🏠")
local PlayerTab = EliteHub:CreateTab(GameMenu, "Игрок", "👤")
local WorldTab = EliteHub:CreateTab(GameMenu, "Мир", "🌍")

-- Секция автоФарма
local AutoFarmSection = EliteHub:CreateSection(MainTab, "Авто-Фарм")

local FarmToggle = EliteHub:CreateToggle(AutoFarmSection, "Авто-фарм монет", false, function(State)
    if State then
        EliteHub:Notify("Авто-фарм", "Запущен! 💰", 2, "Success")
        -- Код фарма
    else
        EliteHub:Notify("Авто-фарм", "Остановлен", 2, "Info")
    end
end)

local FarmSpeed = EliteHub:CreateSlider(AutoFarmSection, "Скорость фарма", 1, 10, 5, function(Value)
    EliteHub:Notify("Скорость", "Установлена: " .. Value, 1, "Info")
end)

-- Секция игрока
local PlayerSection = EliteHub:CreateSection(PlayerTab, "Характеристики")

local SpeedSlider = EliteHub:CreateSlider(PlayerSection, "Скорость", 16, 200, 16, function(Value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
end)

local JumpSlider = EliteHub:CreateSlider(PlayerSection, "Прыжок", 50, 200, 50, function(Value)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
end)

-- Кнопки телепортации
local TeleportSection = EliteHub:CreateSection(WorldTab, "Телепорты")

EliteHub:CreateButton(TeleportSection, "Спавн", function()
    -- Код телепортации на спавн
    EliteHub:Notify("Телепорт", "Перенос на спавн...", 2, "Info")
end)

EliteHub:CreateButton(TeleportSection, "Арена", function()
    -- Код телепортации на арену
    EliteHub:Notify("Телепорт", "Перенос на арену...", 2, "Info")
end)

🎯 ПРИМЕР 2: АДМИН ПАНЕЛЬ
lua

local AdminPanel = EliteHub:CreateWindow("Admin Panel")
EliteHub:CreateOpenButton(AdminPanel)

local ModerationTab = EliteHub:CreateTab(AdminPanel, "Модерация", "🛡️")
local ToolsTab = EliteHub:CreateTab(AdminPanel, "Инструменты", "🔧")

-- Модерация
local KickSection = EliteHub:CreateSection(ModerationTab, "Управление игроками")

-- Выпадающий список игроков (имитация)
local Players = game.Players:GetPlayers()
for _, player in ipairs(Players) do
    EliteHub:CreateButton(KickSection, "Кикнуть " .. player.Name, function()
        EliteHub:Notify("Модерация", "Игрок " .. player.Name .. " кикнут", 3, "Warning")
    end)
end

-- Инструменты
local ToolsSection = EliteHub:CreateSection(ToolsTab, "Серверные инструменты")

EliteHub:CreateToggle(ToolsSection, "Бессмертие", false, function(State)
    if State then
        game.Players.LocalPlayer.Character.Humanoid.Health = math.huge
    end
end)

EliteHub:CreateButton(ToolsSection, "Очистить карту", function()
    EliteHub:Notify("Инструменты", "Очистка карты...", 3, "Danger")
end)

🎯 ПРИМЕР 3: ВИЗУАЛЬНЫЕ НАСТРОЙКИ
lua

local VisualMenu = EliteHub:CreateWindow("Visual Settings")
EliteHub:CreateOpenButton(VisualMenu)

local GraphicsTab = EliteHub:CreateTab(VisualMenu, "Графика", "🎨")
local EffectsTab = EliteHub:CreateTab(VisualMenu, "Эффекты", "✨")

-- Настройки графики
local QualitySection = EliteHub:CreateSection(GraphicsTab, "Качество")

local ShadowsToggle = EliteHub:CreateToggle(QualitySection, "Тени", true, function(State)
    -- Код включения/выключения теней
end)

local ParticlesSlider = EliteHub:CreateSlider(QualitySection, "Частицы", 0, 100, 50, function(Value)
    -- Код настройки частиц
end)

-- Визуальные эффекты
local ESPToggle = EliteHub:CreateToggle(EffectsTab, "ESP игроков", false, function(State)
    EliteHub:Notify("ESP", State and "Включено 👁️" or "Выключено", 2, "Info")
end)

local TracerToggle = EliteHub:CreateToggle(EffectsTab, "Трейсеры", false, function(State)
    EliteHub:Notify("Трейсеры", State and "Включены 🎯" or "Выключены", 2, "Info")
end)

7. СОВЕТЫ И ЛУЧШИЕ ПРАКТИКИ
🎯 СОВЕТ 1: ОРГАНИЗАЦИЯ КОДА
lua

-- ❌ ПЛОХО - все в одном месте
local Window = EliteHub:CreateWindow("Меню")
EliteHub:CreateOpenButton(Window)
local Tab1 = EliteHub:CreateTab(Window, "Таб1", "1")
-- ... много кода ...

-- ✅ ХОРОШО - структурированный код
local function CreateMainWindow()
    local Window = EliteHub:CreateWindow("Мое меню")
    EliteHub:CreateOpenButton(Window)
    return Window
end

local function SetupTabs(Window)
    local MainTab = EliteHub:CreateTab(Window, "Главная", "🏠")
    local SettingsTab = EliteHub:CreateTab(Window, "Настройки", "⚙️")
    return {Main = MainTab, Settings = SettingsTab}
end

local function AddMainTabElements(Tab)
    EliteHub:CreateSection(Tab, "Основные функции")
    -- Добавление элементов...
end

-- Основной код
local MyWindow = CreateMainWindow()
local Tabs = SetupTabs(MyWindow)
AddMainTabElements(Tabs.Main)

🎯 СОВЕТ 2: ОБРАБОТКА ОШИБОК
lua

-- Безопасное создание элементов
local function SafeCreateButton(tab, text, callback)
    local success, err = pcall(function()
        EliteHub:CreateButton(tab, text, callback)
    end)
    
    if not success then
        EliteHub:Notify("Ошибка", "Не удалось создать кнопку: " .. text, 3, "Danger")
        warn("Ошибка создания кнопки: " .. err)
    end
end

-- Использование
SafeCreateButton(MainTab, "Важная кнопка", function()
    -- код кнопки
end)

🎯 СОВЕТ 3: ОПТИМИЗАЦИЯ ПРОИЗВОДИТЕЛЬНОСТИ
lua

-- Используйте отложенную загрузку для тяжелых функций
local HeavyTab = EliteHub:CreateTab(Window, "Тяжелые скрипты", "⚡")

EliteHub:CreateButton(HeavyTab, "Загрузить тяжелый скрипт", function()
    EliteHub:Notify("Загрузка", "Загружаем тяжелые ресурсы...", 2, "Info")
    
    -- Имитация тяжелой загрузки
    wait(2)
    
    -- Только после клика загружаем тяжелый код
    local HeavyModule = require(123456789) -- Пример
    HeavyModule:Initialize()
    
    EliteHub:Notify("Успех", "Тяжелый скрипт загружен! 🎉", 3, "Success")
end)

🎯 СОВЕТ 4: КАСТОМИЗАЦИЯ ЦВЕТОВ
lua

-- Создание своей цветовой схемы
local CustomColors = {
    Background = Color3.fromRGB(20, 20, 40),    -- Темно-синий
    Secondary = Color3.fromRGB(30, 30, 60),     -- Синий
    Accent = Color3.fromRGB(0, 255, 200),       -- Бирюзовый
    Text = Color3.fromRGB(255, 255, 255),       -- Белый
    Success = Color3.fromRGB(0, 255, 150),      -- Зелено-бирюзовый
    Danger = Color3.fromRGB(255, 100, 100),     -- Красный
}

-- Временная замена цветов (если библиотека позволяет)
local originalColors = EliteHub.Colors
EliteHub.Colors = CustomColors

-- Не забудьте вернуть оригинальные цвета если нужно
-- EliteHub.Colors = originalColors

🎓 ЗАКЛЮЧЕНИЕ

Elite Hub предоставляет все необходимые инструменты для создания профессиональных интерфейсов в Roblox. Ключевые преимущества:

    ✅ Простота использования - интуитивный API

    ✅ Богатые возможности - все необходимые элементы UI

    ✅ Красивый дизайн - современный внешний вид

    ✅ Гибкость - легко настраивается и расширяется

    ✅ Анимации - плавные и эффектные переходы

🚀 ЧТО ДАЛЬШЕ?

    Экспериментируйте с разными комбинациями элементов

    Изучайте документацию Roblox UI

    Создавайте свои кастомные компоненты

    Оптимизируйте производительность тяжелых интерфейсов

Удачи в создании потрясающих интерфейсов с Elite Hub! 🎉
