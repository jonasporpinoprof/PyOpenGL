---

### **Passo 1: Instalar o Visual Studio**
1. **Baixe e instale o Visual Studio** (preferencialmente a versão mais recente).
2. Durante a instalação, selecione a opção **Desenvolvimento para Desktop com C++** para garantir que as ferramentas necessárias sejam instaladas.

---

### **Passo 2: Criar um Novo Projeto**
1. **Abra o Visual Studio**.
2. No menu principal, clique em **Arquivo > Novo > Projeto**.
3. Na janela de criação de projeto:
   - Selecione **Aplicativo de Desktop Windows** (C++).
   - Escolha um nome para o seu projeto (por exemplo, `ExemploDirect3D`).
   - Escolha uma pasta de destino.
4. Clique em **Criar**.

---

### **Passo 3: Adicionar as Bibliotecas do Direct3D**
1. **No Gerenciador de Soluções** (Solution Explorer), clique com o botão direito no projeto e selecione **Propriedades**.
2. No menu lateral, vá até **Vinculador > Entrada**.
3. No campo **Dependências Adicionais**, adicione as seguintes bibliotecas:
   - `d3d11.lib`
   - `dxgi.lib`
   - `d3dcompiler.lib`

---

### **Passo 4: Configurar a Janela para Renderização**
1. No arquivo `main.cpp` gerado automaticamente pelo projeto, remova o código padrão e substitua-o pelo código abaixo:

```cpp
#include <windows.h>
#include <d3d11.h>
#include <dxgi.h>

// Ponteiros Direct3D
ID3D11Device* device = nullptr;
ID3D11DeviceContext* context = nullptr;
IDXGISwapChain* swapChain = nullptr;
ID3D11RenderTargetView* renderTargetView = nullptr;

// Função para inicializar Direct3D
bool InitializeDirect3D(HWND hwnd) {
    DXGI_SWAP_CHAIN_DESC swapChainDesc = {};
    swapChainDesc.BufferCount = 1;
    swapChainDesc.BufferDesc.Width = 800;       // Largura da janela
    swapChainDesc.BufferDesc.Height = 600;      // Altura da janela
    swapChainDesc.BufferDesc.Format = DXGI_FORMAT_R8G8B8A8_UNORM;
    swapChainDesc.BufferUsage = DXGI_USAGE_RENDER_TARGET_OUTPUT;
    swapChainDesc.OutputWindow = hwnd;
    swapChainDesc.SampleDesc.Count = 4;         // Anti-aliasing
    swapChainDesc.Windowed = TRUE;              // Janela

    // Criação do dispositivo Direct3D, contexto e swap chain
    HRESULT hr = D3D11CreateDeviceAndSwapChain(
        nullptr, D3D_DRIVER_TYPE_HARDWARE, nullptr, 0, nullptr, 0,
        D3D11_SDK_VERSION, &swapChainDesc, &swapChain, &device, nullptr, &context);
    if (FAILED(hr)) {
        return false;
    }

    // Criar Render Target View
    ID3D11Texture2D* backBuffer = nullptr;
    swapChain->GetBuffer(0, __uuidof(ID3D11Texture2D), (void**)&backBuffer);
    device->CreateRenderTargetView(backBuffer, nullptr, &renderTargetView);
    context->OMSetRenderTargets(1, &renderTargetView, nullptr);
    backBuffer->Release();

    return true;
}

// Função de renderização (limpa a tela)
void Render() {
    float clearColor[] = { 0.0f, 0.2f, 0.4f, 1.0f };  // Cor de fundo
    context->ClearRenderTargetView(renderTargetView, clearColor);
    swapChain->Present(0, 0);  // Apresenta o buffer
}

// Função de callback da janela
LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam) {
    switch (uMsg) {
    case WM_DESTROY:
        PostQuitMessage(0);
        return 0;
    }
    return DefWindowProc(hwnd, uMsg, wParam, lParam);
}

// Função principal
int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE, LPSTR, int nCmdShow) {
    WNDCLASSEX wc = { sizeof(WNDCLASSEX), CS_CLASSDC, WindowProc, 0L, 0L, GetModuleHandle(NULL), NULL, NULL, NULL, NULL, "Direct3DWindow", NULL };
    RegisterClassEx(&wc);
    HWND hwnd = CreateWindow(wc.lpszClassName, "Exemplo Direct3D", WS_OVERLAPPEDWINDOW, 100, 100, 800, 600, NULL, NULL, wc.hInstance, NULL);

    if (!InitializeDirect3D(hwnd)) {
        return -1;  // Se Direct3D falhar
    }

    ShowWindow(hwnd, nCmdShow);
    UpdateWindow(hwnd);

    MSG msg = {};
    while (msg.message != WM_QUIT) {
        if (PeekMessage(&msg, NULL, 0U, 0U, PM_REMOVE)) {
            TranslateMessage(&msg);
            DispatchMessage(&msg);
        } else {
            Render();  // Chama a função de renderização
        }
    }

    // Limpeza
    renderTargetView->Release();
    swapChain->Release();
    context->Release();
    device->Release();

    return 0;
}
```

---

### **Passo 5: Compilar e Executar o Projeto**
1. **Compile o projeto** clicando em **Compilar > Compilar Solução**.
2. **Execute o projeto** clicando em **Depurar > Iniciar Sem Depuração**.

Se tudo estiver correto, uma janela de 800x600 será aberta com uma tela de fundo azul. Esta é a tela renderizada pelo Direct3D.

---

### **Passo 6: Expansão e Exploração**
Agora que você tem um projeto básico de Direct3D rodando, você pode:
- Explorar **shaders** para renderizar gráficos 3D mais complexos.
- Adicionar **texturas** e **modelos 3D**.
- Trabalhar com **movimentação de câmera** e outros elementos interativos.

---

Esse passo a passo inicializa o Direct3D de forma simples no Visual Studio em português, permitindo que você comece a criar gráficos 3D!
