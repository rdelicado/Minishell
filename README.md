# 🖥️ Minishell

[![Language](https://img.shields.io/badge/Language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Shell](https://img.shields.io/badge/Shell-UNIX_Compatible-green.svg)](https://en.wikipedia.org/wiki/Unix_shell)
[![Readline](https://img.shields.io/badge/Library-GNU_Readline-red.svg)](https://tiswww.case.edu/php/chet/readline/rltop.html)
[![42 School](https://img.shields.io/badge/42-School_Project-purple.svg)](https://42.fr/)

## 📋 Description

**Minishell** es un intérprete de comandos UNIX que recrea las funcionalidades esenciales de bash. Este proyecto demuestra el dominio de la programación de sistemas, gestión de procesos, manejo de señales y análisis sintáctico, proporcionando una experiencia de shell completa y funcional.

Desarrollado en C con la biblioteca GNU Readline, Minishell implementa un lexer/parser completo, ejecución de comandos, redirecciones, pipes, variables de entorno y comandos integrados, manteniendo la compatibilidad POSIX.

## 🚀 Features

### Core Shell Features
- **Interactive Shell**: Prompt persistente con historial de comandos
- **Command Execution**: Ejecución de comandos del sistema con resolución de PATH
- **Pipes**: Conexión de comandos con `|` para procesamiento en cadena
- **Redirections**: Redirección de entrada (`<`) y salida (`>`, `>>`)
- **Environment Variables**: Expansión y gestión de variables (`$VAR`, `$?`)
- **Quote Handling**: Soporte para comillas simples y dobles

### Built-in Commands
- **echo** (con flag `-n`)
- **cd** (con rutas relativas/absolutas y `~`, `-`)
- **pwd** 
- **export**
- **unset**
- **env**
- **exit** (con código de estado opcional)

### Advanced Features
- **Signal Handling**: Gestión de SIGINT (Ctrl+C) y SIGQUIT (Ctrl+\)
- **Command History**: Navegación con readline (↑/↓)
- **Error Handling**: Mensajes de error descriptivos
- **Memory Management**: Sin memory leaks

## 🛠️ Installation

### Prerequisites
```bash
# Ubuntu/Debian
sudo apt-get install libreadline-dev build-essential

# macOS
brew install readline
```

### Compilation
```bash
git clone https://github.com/rdelicado/Minishell.git
cd Minishell
make
```

## 🚀 Usage

### Basic Examples
```bash
# Start Minishell
./minishell

# Basic commands
minishell$ ls -la
minishell$ pwd
minishell$ echo "Hello World"

# Built-ins
minishell$ export MY_VAR=value
minishell$ echo $MY_VAR
minishell$ cd /tmp
minishell$ pwd

# Pipes and redirections
minishell$ ls | grep .c
minishell$ echo "test" > file.txt
minishell$ cat < file.txt

# Complex pipelines
minishell$ ps aux | grep minishell | wc -l
```

### Environment Variables
```bash
minishell$ export PATH="/usr/local/bin:$PATH"
minishell$ echo "User: $USER"
minishell$ echo "Exit status: $?"
```

## 📁 Project Structure

```
Minishell/
├── Makefile
├── include/
│   ├── minishell.h
│   ├── minishell_structs.h
│   ├── minishell_functions.h
│   └── libft/
├── src/
│   ├── main.c                    # Entry point
│   ├── l_*.c                     # Lexer (tokenization)
│   ├── p_*.c                     # Parser (syntax analysis)
│   ├── exec.c                    # Command execution
│   ├── b_*.c                     # Built-in commands
│   ├── s_signal.c                # Signal handling
│   └── free.c                    # Memory management
└── objs/                         # Generated object files
```

## 🧪 Testing

### Test Examples
```bash
# Basic functionality
echo "pwd" | ./minishell
echo "echo hello" | ./minishell

# Pipes and redirections
echo "ls | wc -l" | ./minishell
echo "echo test > /tmp/test && cat /tmp/test" | ./minishell

# Environment handling
echo -e "export TEST=value\necho \$TEST" | ./minishell

# Error cases
echo "/nonexistent/command" | ./minishell
```

### Memory Testing
```bash
# Check for memory leaks
valgrind --leak-check=full ./minishell

# Build with address sanitizer
make re CFLAGS="-fsanitize=address"
```

## 🚨 Common Issues

### Readline Installation
```bash
# Ubuntu/Debian
sudo apt-get install libreadline-dev

# macOS with Homebrew
brew install readline
export LDFLAGS="-L$(brew --prefix readline)/lib"
```

### Signal Handling
El shell maneja correctamente Ctrl+C (SIGINT) sin terminar el proceso principal, y Ctrl+\ (SIGQUIT) se ignora como en bash.

### Memory Management
Toda la memoria asignada dinámicamente se libera correctamente. Use `make debug` para compilar con AddressSanitizer.

## 📊 Implementation Highlights

### Architecture
- **Lexer**: Tokenización de entrada en símbolos (palabras, operadores, redirecciones)
- **Parser**: Análisis sintáctico para construir árbol de comandos
- **Executor**: Ejecución con fork/execve y gestión de pipes/redirecciones
- **Built-ins**: Comandos integrados ejecutados directamente en el shell

### Key Features
- Gestión completa de procesos hijo con wait()
- Resolución automática de PATH para ejecutables
- Manejo robusto de señales en modo interactivo
- Expansión de variables de entorno en tiempo real
- Sintaxis compatible con bash para operaciones básicas

## 👨‍💻 Authors

- **Rubén Delicado** - [@rdelicado](https://github.com/rdelicado)
- **Pablo Lucena** - [@palucena](https://github.com/palucena)

*42 Málaga - System Programming Project*

## 📜 License

This project is part of the 42 School curriculum. Educational use only.

---

*A minimal yet powerful UNIX shell implementation demonstrating mastery of system programming concepts in C.*