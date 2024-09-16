### Aula 06 -  Computação Gráfica: Introdução ao PyOpenGL

#### Objetivo:
Nesta aula, você aprenderá o que é o **PyOpenGL**, como instalá-lo em sistemas operacionais Linux e Windows, além de ver um exemplo prático de uso. Ao final, você deverá ser capaz de criar aplicações gráficas 3D simples usando Python e PyOpenGL.

---

### 1. O que é o PyOpenGL?

O **PyOpenGL** é uma biblioteca Python que fornece acesso às funcionalidades do OpenGL, uma API padrão para renderização de gráficos 2D e 3D. Ele é amplamente utilizado em desenvolvimento de jogos, simulações gráficas e renderização científica.

---

### 2. Pré-requisitos

- Conhecimento básico de Python.
- Noções básicas de gráficos 3D (opcional).

---

### 3. Instalação do PyOpenGL

#### 3.1. Instalação no Linux

Existem duas maneiras principais de instalar o PyOpenGL no Linux: usando o gerenciador de pacotes do sistema (como `zypper`, `apt` ou `dnf`), ou instalando através do `pip` em um ambiente virtual. Vamos cobrir ambos os métodos.

##### 3.1.1. Usando o Gerenciador de Pacotes (exemplo: openSUSE com `zypper`)
1. Abra um terminal.
2. Instale o PyOpenGL com o seguinte comando:

   ```bash
   sudo zypper install python311-PyOpenGL
   ```

##### 3.1.2. Usando um Ambiente Virtual

Se preferir instalar o PyOpenGL sem modificar o sistema, siga os passos para criar um ambiente virtual:

1. Crie um ambiente virtual:
   ```bash
   python3.11 -m venv /caminho/para/venv
   ```

2. Ative o ambiente virtual:
   ```bash
   source /caminho/para/venv/bin/activate
   ```

3. Instale o PyOpenGL e sua aceleração:
   ```bash
   pip install PyOpenGL PyOpenGL_accelerate
   ```

Agora, o PyOpenGL está instalado e pronto para ser utilizado no seu ambiente virtual.

#### 3.2. Instalação no Windows

##### 3.2.1. Instalando com `pip`

1. Certifique-se de ter o **Python** e o **pip** instalados. Se ainda não tiver, baixe e instale a versão mais recente do [site oficial do Python](https://www.python.org/downloads/).
   
2. Abra o **Prompt de Comando** (cmd) ou **PowerShell**.

3. Execute o comando para instalar o PyOpenGL e o PyOpenGL_accelerate:
   ```bash
   pip install PyOpenGL PyOpenGL_accelerate
   ```

Agora você já pode utilizar o PyOpenGL no seu ambiente Python do Windows.

##### 3.2.2. Instalando um Ambiente Virtual (Opcional)

Se você preferir usar um ambiente virtual no Windows, siga os passos:

1. Crie um ambiente virtual:
   ```bash
   python -m venv C:\caminho\para\venv
   ```

2. Ative o ambiente virtual:
   ```bash
   C:\caminho\para\venv\Scripts\activate
   ```

3. Instale o PyOpenGL:
   ```bash
   pip install PyOpenGL PyOpenGL_accelerate
   ```

---

### 4. Exemplo de Uso do PyOpenGL

Agora que o PyOpenGL está instalado, vamos criar um exemplo básico de uma janela com um cubo 3D.

#### 4.1. Código: Exemplo de Cubo 3D

Este exemplo cria uma janela e renderiza um cubo rotativo usando o **PyOpenGL**.

```python
import pygame
from pygame.locals import *
from OpenGL.GL import *
from OpenGL.GLU import *

vertices = (
    (1, -1, -1),
    (1, 1, -1),
    (-1, 1, -1),
    (-1, -1, -1),
    (1, -1, 1),
    (1, 1, 1),
    (-1, -1, 1),
    (-1, 1, 1)
)

edges = (
    (0, 1),
    (1, 2),
    (2, 3),
    (3, 0),
    (4, 5),
    (5, 6),
    (6, 7),
    (7, 4),
    (0, 4),
    (1, 5),
    (2, 6),
    (3, 7)
)

def draw_cube():
    glBegin(GL_LINES)
    for edge in edges:
        for vertex in edge:
            glVertex3fv(vertices[vertex])
    glEnd()

def main():
    pygame.init()
    display = (800, 600)
    pygame.display.set_mode(display, DOUBLEBUF | OPENGL)
    gluPerspective(45, (display[0] / display[1]), 0.1, 50.0)
    glTranslatef(0.0, 0.0, -5)

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                quit()

        glRotatef(1, 3, 1, 1)
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
        draw_cube()
        pygame.display.flip()
        pygame.time.wait(10)

if __name__ == "__main__":
    main()
```

#### 4.2. Executando o Exemplo

- **Linux:** Execute o arquivo Python no terminal:
  ```bash
  python3 teste.py
  ```

- **Windows:** No Prompt de Comando, navegue até o diretório do arquivo e execute:
  ```bash
  python teste.py
  ```

---

### 5. Resumo

- O **PyOpenGL** permite criar gráficos 2D e 3D usando Python.
- No **Linux**, o PyOpenGL pode ser instalado via `zypper` ou em um ambiente virtual.
- No **Windows**, a instalação pode ser feita diretamente com `pip`.
- Um exemplo prático de cubo 3D foi apresentado para ilustrar o uso do PyOpenGL com o **Pygame** para criar uma janela gráfica.

---

### 6. Atividades

1. Instale o PyOpenGL no seu sistema (Linux ou Windows).
2. Execute o exemplo do cubo 3D.
3. Experimente modificar as dimensões e cores do cubo.
4. Crie uma nova forma geométrica, como uma pirâmide ou esfera.

---

Isso conclui a aula sobre PyOpenGL!
