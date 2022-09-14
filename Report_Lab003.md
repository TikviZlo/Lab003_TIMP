## Задание 1

Вам поручили перейти на систему автоматизированной сборки CMake. Исходные файлы находятся в директории formatter_lib. В этой директории находятся файлы для статической библиотеки formatter. Создайте CMakeList.txt в директории formatter_lib, с помощью которого можно будет собирать статическую библиотеку formatter.

# Решение:

1. Создаём CMakeLists.txt для данной библиотеки:

```
$ touch CMake.Lists.txt
$ cat >CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.10)
> 
> set(CMAKE_CXX_STANDARD 11)
> set(CMAKE_CXX_STANDARD_REQUIRED True)
> 
> project(formatter)
> 
> add_library(formatter STATIC formatter.cpp formatter.h)
> EOF

```

2. Cобираем библиотеку:

```
cmake -H. -B_build && cmake --build _build
```

<details>

<summary>Вывод:</summary>

```
-- Building for: Visual Studio 17 2022
-- Selecting Windows SDK version 10.0.19041.0 to target Windows 10.0.22000.
-- The C compiler identification is MSVC 19.32.31329.0
-- The CXX compiler identification is MSVC 19.32.31329.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Users/inna2/OneDrive/Документы/ГитПроекты/Lab003_TIMP/formatter_lib/_build
```

</details>

## Задание 2

У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием CMakeList.txt для статической библиотеки formatter, ваш руководитель поручает заняться созданием CMakeList.txt для библиотеки formatter_ex, которая в свою очередь использует библиотеку formatter.

# Решение:

1. Создаём CMakeLists.txt для следующей библиотеки:

```
cat > CMakeLists.txt <<EOF
>cmake_minimum_required(VERSION 3.10)
> 
> project(formatter_ex)
> 
> set(CMAKE_CXX_STANDARD 11)
> set(CMAKE_CXX_STANDARD_REQUIRED True)
> 
> include_directories("../formatter_lib")
> 
> add_library(formatter_ex STATIC formatter_ex.cpp formatter_ex.h)
> 
> target_link_libraries(formatter_ex formatter)
> EOF
```

2. Собираем библиотеку:

<details>

<summary>Вывод:</summary>

```
-- Building for: Visual Studio 17 2022
-- Selecting Windows SDK version 10.0.19041.0 to target Windows 10.0.22000.
-- The C compiler identification is MSVC 19.32.31329.0
-- The CXX compiler identification is MSVC 19.32.31329.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Users/inna2/OneDrive/Документы/ГитПроекты/Lab003_TIMP/formatter_ex_lib/_build
```

</details>


## Задание 3

Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой formatter_ex, вам необходимо создать два CMakeList.txt для двух простых приложений:

hello_world, которое использует библиотеку formatter_ex;
solver, приложение которое испольует статические библиотеки formatter_ex и solver_lib.

Удачной стажировки!

# Решение:

1. Заполняем CMakeLists для hello_world:

```
$ cat >CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.10)
> 
> project(hello_world)
> 
> set(CMAKE_CXX_STANDARD 11)
> set(CMAKE_CXX_STANDARD_REQUIRED True)
> 
> include_directories("../formatter_ex_lib")
> include_directories("../formatter_lib")
> 
> add_library(formatter STATIC "../formatter_lib/formatter.cpp" "../formatter_lib/formatter.h")
> EOF
```

2. Строим hello_world:

```
$ cmake -H. -B_build && cmake --build _build
```

<details>

<summary>Вывод:</summary>

```
-- Building for: Visual Studio 17 2022
-- Selecting Windows SDK version 10.0.19041.0 to target Windows 10.0.22000.
-- The C compiler identification is MSVC 19.32.31329.0
-- The CXX compiler identification is MSVC 19.32.31329.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Users/inna2/OneDrive/Документы/ГитПроекты/Lab003_TIMP/hello_world_application/_build
```

</details>

3. Собираем библиотеку solver:

```
$ cmake -H. -B_build && cmake --build _build
```

<details>

<summary>Вывод:</summary>

```
-- Building for: Visual Studio 17 2022
-- Selecting Windows SDK version 10.0.19041.0 to target Windows 10.0.22000.
-- The C compiler identification is MSVC 19.32.31329.0
-- The CXX compiler identification is MSVC 19.32.31329.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Users/inna2/OneDrive/Документы/ГитПроекты/Lab003_TIMP/solver_lib/_build
```

</details>

4. Делаем CMakeLists.txt для самого приложения:

```
cmake_minimum_required(VERSION 3.10)

project(solver_app)

include_directories("../formatter_lib")
include_directories("../formatter_ex_lib")
include_directories("../solver_lib")

add_library(formatter STATIC "../formatter_lib/formatter.cpp" "../formatter_lib/formatter.h")
add_library(formatter_ex STATIC "../formatter_ex_lib/formatter_ex.cpp" "../formatter_ex_lib/formatter_ex.h")
add_library(solver STATIC "../solver_lib/solver.cpp" "../solver_lib/solver.h")

add_executable(solver_app equation.cpp)

target_link_libraries(solver_app formatter_ex formatter solver)
```

5. Собираем приложение solver:


```
$ cmake -H. -B_build && cmake --build _build
```

<details>

<summary>Вывод:</summary>

```
-- Building for: Visual Studio 17 2022
-- Selecting Windows SDK version 10.0.19041.0 to target Windows 10.0.22000.
-- The C compiler identification is MSVC 19.32.31329.0
-- The CXX compiler identification is MSVC 19.32.31329.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/bin/Hostx64/x64/cl.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Users/inna2/OneDrive/Документы/ГитПроекты/Lab003_TIMP/solver_application/_build

```

</details>