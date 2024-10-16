### Aula 06 -  Computação Gráfica: Introdução ao PyOpenGL

**OpenGL** (Open Graphics Library) é uma API (Interface de Programação de Aplicações) padrão e amplamente utilizada para desenvolver gráficos 2D e 3D. Foi criada para facilitar a criação de imagens, cenas e animações com qualidade gráfica elevada, oferecendo uma maneira eficiente de interagir com o hardware gráfico.

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


 ## Instale o PyOpenGL:
   ```bash
   pip install PyOpenGL PyOpenGL_accelerate
   ```

---

### Exemplo de Uso do PyOpenGL

Agora que o PyOpenGL está instalado, vamos criar um exemplo básico de uma janela com um cubo 3D.

#### Código: Exemplo de Cubo 3D

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
    (5, 6), # Modifique
    (6, 7),
    (7, 4), # Modifique
    (0, 4),
    (1, 5),
    (2, 6), # Modifique
    (3, 7)  # Modifique
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


## Explicação sobre o Código

Este código usa as bibliotecas `Pygame` e `PyOpenGL` para criar uma janela e renderizar um cubo 3D rotativo. Vou explicar o código em partes:

### Importações
```python
import pygame
from pygame.locals import *
from OpenGL.GL import *
from OpenGL.GLU import *
```
- `pygame`: Biblioteca para criar janelas e gerenciar eventos.
- `pygame.locals`: Contém constantes como `DOUBLEBUF` e `OPENGL` que são usadas para criar a janela com buffers duplos e suporte OpenGL.
- `OpenGL.GL` e `OpenGL.GLU`: Funções e constantes do OpenGL para renderização gráfica e utilitários OpenGL, como `glVertex3fv` (para definir vértices) e `gluPerspective` (para definir a perspectiva da câmera).

### Definição de Vértices e Arestas
```python
vertices = (
    (1, -1, -1), (1, 1, -1), (-1, 1, -1), (-1, -1, -1),
    (1, -1, 1), (1, 1, 1), (-1, -1, 1), (-1, 1, 1)
)
```
- Estes são os vértices que definem os 8 cantos do cubo no espaço 3D.
  - Cada tupla representa um ponto no espaço tridimensional (x, y, z).

```python
edges = (
    (0, 1),
    (1, 2),
    (2, 3),
    (3, 0),
    (4, 5),
    (5, 6), # Modifique
    (6, 7),
    (7, 4), # Modifique
    (0, 4),
    (1, 5),
    (2, 6), # Modifique
    (3, 7)  # Modifique
)
```
- `edges` contém pares de índices que definem as 12 arestas do cubo, onde cada índice se refere a um vértice da lista `vertices`.
- As arestas são os segmentos de linha que conectam dois vértices.

### Função `draw_cube`
```python
def draw_cube():
    glBegin(GL_LINES)
    for edge in edges:
        for vertex in edge:
            glVertex3fv(vertices[vertex])
    glEnd()
```
- Esta função desenha o cubo.
- `glBegin(GL_LINES)` diz ao OpenGL para começar a desenhar linhas.
- Para cada aresta em `edges`, ela acessa os vértices correspondentes e os passa para `glVertex3fv`, que define os pontos no espaço 3D.
- `glEnd()` finaliza o desenho das linhas.

### Função `main`
```python
def main():
    pygame.init()
    display = (800, 600)
    pygame.display.set_mode(display, DOUBLEBUF | OPENGL)
```
- Inicializa o `pygame` e cria uma janela com tamanho 800x600 pixels, usando buffers duplos (`DOUBLEBUF`) para suavizar a animação e suporte OpenGL (`OPENGL`).

```python
    gluPerspective(45, (display[0] / display[1]), 0.1, 50.0)
    glTranslatef(0.0, 0.0, -5)
```
- `gluPerspective(45, ...)`: Define a perspectiva de visualização da câmera. O primeiro argumento é o campo de visão (45 graus), o segundo é a proporção da tela (largura/altura), e os dois últimos valores são o plano de corte próximo (0.1) e o plano de corte distante (50.0).
- `glTranslatef(0.0, 0.0, -5)`: Move a cena para trás no eixo Z, para que o cubo fique visível.

### Loop Principal
```python
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                quit()
```
- Este loop captura eventos do `pygame`. Se o evento `QUIT` (fechamento da janela) for detectado, o programa encerra.

```python
        glRotatef(1, 3, 1, 1)
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
        draw_cube()
        pygame.display.flip()
        pygame.time.wait(10)
```
- `glRotatef(1, 3, 1, 1)`: Rota a cena em torno dos eixos X, Y e Z. Neste caso, o cubo está girando de forma contínua.
- `glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)`: Limpa o buffer de cor e o buffer de profundidade antes de desenhar o próximo quadro.
- `draw_cube()`: Desenha o cubo.
- `pygame.display.flip()`: Atualiza a tela com o que foi desenhado.
- `pygame.time.wait(10)`: Pausa a execução por 10 milissegundos, controlando a velocidade da animação.

### Resumo
Este código cria uma janela usando `Pygame` e renderiza um cubo 3D rotativo com `OpenGL`, utilizando vértices e arestas definidos manualmente. O cubo é desenhado usando linhas (`GL_LINES`) para representar suas arestas, e a perspectiva da câmera é configurada com `gluPerspective`.
