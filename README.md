# Fortnite Picker

Lista przedmiotów z Fortnite połączona z trójwymiarową przeglądarką [Snooper](https://github.com/FModel/Snooper): klikasz przedmiot, a jego model od razu pojawia się w oknie Snoopera.

Program nie jest powiązany z Epic Games, Inc. ani przez nią wspierany. Fortnite jest znakiem towarowym Epic Games, Inc. Program nie zawiera plików gry.

## Wymagania

- Windows 10 lub 11 (64-bitowy)
- Fortnite zainstalowany przez Epic Games Launcher
- Karta graficzna z OpenGL 4.6 i obsługą bindless textures
- Około 3 GB wolnej pamięci RAM i kilka GB miejsca na dysku
- Połączenie z internetem

## Instalacja

1. Pobierz paczkę `FortnitePicker-…-win-x64.zip`.
2. Rozpakuj ją w dowolnym folderze.
3. Uruchom `FortnitePicker.exe`. .NET nie trzeba instalować.

Program nie ma podpisu cyfrowego, więc Windows może pokazać ostrzeżenie SmartScreen. Żeby uruchomić go mimo to, wybierz „Więcej informacji”, a potem „Uruchom mimo to”.

Pierwsze uruchomienie pobiera około 340 MB i trwa około pół minuty. Kolejne trwają kilkanaście sekund.

## Obsługa

- Wyszukiwarka działa po polsku i angielsku, także bez polskich znaków.
- W Snooperze przytrzymaj prawy przycisk myszy, żeby obracać kamerą wokół przedmiotu.
- Klawisz Esc w oknie Snoopera zamyka program.

Można wybierać stroje, plecaki, kilofy, lotnie, emotki, buty, towarzyszy, zwierzaki i zabawki. Emotka gra na ostatnio wybranym stroju, a gdy żadnego nie wybrano, na Jonesym.

Na liście nie ma przedmiotów bez modelu 3D, takich jak spraye, malowania i ekrany ładowania, ani broni z gry. Stroje pokazują się w domyślnym stylu, a emotki nie mają dźwięku.

## Skąd program bierze dane

Program działa bez logowania i nie korzysta z konta Epic.

| Dane | Źródło | Kiedy |
| --- | --- | --- |
| Lista przedmiotów, ikony, klucze AES | [fortnite-api.com](https://fortnite-api.com) | Klucze przy każdym starcie, lista raz na dobę, ikony przy przewijaniu |
| Plik mappings | uedb.dev | Gdy pojawi się nowa wersja gry |
| Modele i tekstury spoza dysku | download.epicgames.com | Przy wyborze przedmiotu |
| Biblioteka Oodle | [WorkingRobot/OodleUE](https://github.com/WorkingRobot/OodleUE) | Przy pierwszym uruchomieniu, ze sprawdzeniem sumy kontrolnej |
| Biblioteka zlib-ng | [NotOfficer/Zlib-ng.NET](https://github.com/NotOfficer/Zlib-ng.NET) | Przy pierwszym uruchomieniu, ze sprawdzeniem sumy kontrolnej |

Wszystko trafia do `%LOCALAPPDATA%\FortnitePicker`. Pamięć podręczna fragmentów modeli jest ograniczana do 5 GB przy starcie programu. Folder można bezpiecznie usunąć, wtedy dane pobiorą się ponownie.

Gdy coś nie działa, szczegóły są w pliku `log.txt` w tym samym folderze.

## Po aktualizacji gry

Program sam pobierze nowe klucze i mappings, gdy będą już dostępne. Do tego czasu pasek stanu pokaże ostrzeżenie o różnicy wersji.

Mappings dla wersji 43.00 mają pusty opis klasy `Skeleton`. `Services/MappingFixes.cs` uzupełnia go w pamięci tylko wtedy, gdy jest pusty. Jeśli po aktualizacji emotki przestaną działać, ten opis trzeba sprawdzić w pierwszej kolejności.

Test wszystkich typów przedmiotów zapisuje zrzuty i raport we wskazanym folderze:

```
FortnitePicker.exe --selftest C:\folder\na\wyniki
```

## Budowanie ze źródeł

Potrzebne są .NET 10 SDK oraz Visual Studio z narzędziami C++ albo CMake. Repozytorium trzeba sklonować z podmodułami (`git clone --recursive`), a potem w jego głównym folderze uruchomić:

```
powershell -ExecutionPolicy Bypass -File FortnitePicker\publish.ps1
```

Gotowa paczka pojawi się w folderze `dist`.

## Licencja

GNU GPL w wersji 3, tak jak Snooper. Pełny tekst jest w pliku `LICENSE`, a biblioteki innych autorów i zmiany względem Snoopera są opisane w pliku `NOTICE`. Paczka zawiera dodatkowo `THIRD-PARTY-NOTICES.txt` z listą pakietów NuGet.
