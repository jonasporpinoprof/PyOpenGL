### Aula 06 -  Computação Gráfica: Introdução ao PyOpenGL

O **OpenGL** (Open Graphics Library) é uma API (Interface de Programação de Aplicações) padrão e amplamente utilizada para desenvolver gráficos 2D e 3D. Foi criada para facilitar a criação de imagens, cenas e animações com qualidade gráfica elevada, oferecendo uma maneira eficiente de interagir com o hardware gráfico.

### Características principais do OpenGL:
- **Independência de Plataforma:** Funciona em diversos sistemas operacionais, como Windows, macOS e Linux, além de dispositivos móveis com versões especializadas como OpenGL ES.
- **Independência de Linguagem de Programação:** Embora seja escrita em C, o OpenGL pode ser usado com várias linguagens, como C++, Python (com a biblioteca PyOpenGL), Java e mais.
- **Desempenho Direto:** Ele oferece acesso direto ao hardware gráfico (GPU), o que proporciona alta performance em renderizações e operações gráficas.
- **Modelagem e Renderização 3D:** Suporta a criação de modelos tridimensionais complexos, com ferramentas para aplicar texturas, cores, sombras e outros efeitos visuais.
  
### Como o OpenGL funciona:
O OpenGL trabalha em conjunto com a GPU (Unidade de Processamento Gráfico) para processar gráficos e exibi-los na tela. Ele permite que os desenvolvedores programem gráficos vetoriais, definindo vértices e polígonos, e controlando a forma como os gráficos são renderizados e exibidos.

### Componentes Importantes:
1. **GLU (OpenGL Utility Library):** Uma biblioteca auxiliar que facilita operações mais avançadas, como a criação de câmeras e a projeção de perspectivas.
2. **GLUT (OpenGL Utility Toolkit):** Fornece funções utilitárias para criar janelas, detectar eventos de entrada (como teclado e mouse) e gerenciar a renderização de gráficos.
3. **Shaders:** São pequenos programas que rodam diretamente na GPU e controlam como os gráficos são processados, permitindo criar efeitos de iluminação, sombras e outros efeitos visuais avançados.

### Aplicações do OpenGL:
- **Desenvolvimento de Jogos:** Muitos jogos 3D utilizam OpenGL para renderizar cenas complexas e interativas.
- **Simulações Científicas:** Simulações gráficas, como visualizações de dados ou simulações físicas, usam OpenGL para gerar visualizações 3D.
- **Aplicativos de CAD (Desenho Assistido por Computador):** Softwares de design 3D e modelagem geométrica também utilizam OpenGL para renderização em tempo real.

### Exemplo de uso do OpenGL:
Ao criar gráficos 3D, como um cubo rotacionando, o OpenGL é usado para definir as vértices do cubo, projetá-lo em uma perspectiva 3D e aplicar transformações (como rotação e escalonamento) diretamente na GPU, proporcionando gráficos em alta performance. 

Em resumo, o OpenGL é uma ferramenta fundamental para desenvolvedores que precisam criar gráficos e animações eficientes e interativas, permitindo que eles aproveitem ao máximo os recursos de hardware gráfico disponíveis.

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
Aqui está o código com comentários explicativos:

```python
import pygame
from pygame.locals import *
from OpenGL.GL import *
from OpenGL.GLU import *

# Definindo os vértices do cubo em um espaço tridimensional
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

# Definindo as arestas que conectam os vértices, formando as linhas do cubo
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
    # Iniciando o desenho das linhas
    glBegin(GL_LINES)
    # Desenhando cada aresta do cubo usando os vértices conectados por cada aresta
    for edge in edges:
        for vertex in edge:
            glVertex3fv(vertices[vertex])  # Define a posição do vértice atual
    glEnd()  # Finaliza o desenho das linhas

def main():
    # Inicializando o pygame e configurando a janela com buffer duplo e OpenGL
    pygame.init()
    display = (800, 600)
    pygame.display.set_mode(display, DOUBLEBUF | OPENGL)
    
    # Configurando a perspectiva da câmera
    gluPerspective(45, (display[0] / display[1]), 0.1, 50.0)
    
    # Movendo a câmera para longe do cubo
    glTranslatef(0.0, 0.0, -5)

    # Loop principal do programa
    while True:
        # Gerenciando eventos de saída
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                quit()

        # Rotacionando o cubo um pouco em cada frame
        glRotatef(1, 3, 1, 1)
        
        # Limpando a tela e o buffer de profundidade para atualizar a cena
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
        
        # Chamando a função que desenha o cubo
        draw_cube()
        
        # Atualizando a tela
        pygame.display.flip()
        
        # Atraso para manter a rotação contínua, mas lenta
        pygame.time.wait(10)

if __name__ == "__main__":
    main()
```

Esses comentários explicam o propósito de cada parte do código e como as funções e variáveis se relacionam na criação e exibição de um cubo 3D usando Pygame e OpenGL.
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

### 6. Prática

1. Instale o PyOpenGL no seu sistema (Linux ou Windows).
2. Execute o exemplo do cubo 3D.
3. Experimente modificar as dimensões e cores do cubo. (opcional) 
4. Crie uma nova forma geométrica, como uma pirâmide ou esfera. (opcional)
5. Envie o seu código para seu repositório no GitHub, (pode ser um novo repositório ou um existente)
6. Envie para o seguinte forms: bit.ly/3Xul44j

---

Isso conclui a aula sobre PyOpenGL!
