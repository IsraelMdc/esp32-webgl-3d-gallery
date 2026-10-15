# 🎨 Guia de Integração com Modelos do Blender (.GLB)

A Galeria 3D da Gessy foi desenvolvida em **Three.js** utilizando o módulo oficial `GLTFLoader`. Isso permite que qualquer objeto ou cenário modelado no **Blender** seja inserido na sala de forma simples e com suporte a materiais PBR (Metalness, Roughness, Normal Maps).

---

## 1. Recomendações de Modelagem no Blender

Como o projeto roda em navegadores mobile e pode ser embarcado na memória Flash do ESP32 (LittleFS de 2.62 MB), siga estas diretrizes:

- **Contagem de Polígonos:** Entre **2.000 e 20.000 triângulos (tris)** por modelo.
- **Pivô / Origem:** No Blender, posicione a base do objeto na coordenada `(0, 0, 0)` do grid global antes de exportar. Isso garante que ao posicionar o objeto em $y = 0$, ele fique assentado rente ao piso do salão.
- **Aplicar Transformações:** Sempre selecione o objeto e pressione `Ctrl + A` $\to$ **All Transforms** (Location, Rotation, Scale).
- **Texturas:**
  - Resoluções ideais: `512x512` ou `1024x1024`.
  - Utilize materiais padrão **Principled BSDF** do Blender (eles são convertidos automaticamente para `MeshStandardMaterial` no Three.js).

---

## 2. Passo a Passo de Exportação

1. Selecione o objeto desejado no Blender.
2. Vá em **File > Export > glTF 2.0 (.glb / .gltf)**.
3. Configure as opções do painel lateral direito:
   - **Format:** `glTF Binary (.glb)` *(arquivo binário único contendo malha, materiais e texturas embutidas)*.
   - **Include:** Marque `Selected Objects` (se quiser exportar só o que estiver selecionado).
   - **Transform:** Deixe `+Y Up` ativado (padrão do Three.js).
   - **Geometry:** Marque `Apply Modifiers`.
   - **Images:** Escolha `JPEG Format` ou `Automatic` para compressão máxima.
4. Salve o arquivo na pasta:
   ```text
   modelos/seu_objeto.glb
   ```

---

## 3. Como Carregar o Modelo na Cena 3D

No arquivo [`js/galeria.js`](../js/galeria.js), importe o loader e instancie o modelo:

```javascript
import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";

const loader = new GLTFLoader();

loader.load("modelos/seu_objeto.glb", (gltf) => {
  const objeto = gltf.scene;

  // Ajuste de escala (se necessário)
  objeto.scale.set(0.5, 0.5, 0.5);

  // Posicionamento no salão:
  // X = horizontal, Y = altura em relação ao piso, Z = profundidade
  objeto.position.set(0, 1.0, -2.0);

  // Habilitar sombras e render PBR suave
  objeto.traverse((filho) => {
    if (filho.isMesh) {
      filho.castShadow = true;
      filho.receiveShadow = true;
      if (filho.material) {
        filho.material.envMapIntensity = 0.8;
      }
    }
  });

  cena.add(objeto);
  console.log("✨ Modelo do Blender inserido com sucesso na galeria!");
});
```

---

## 4. Otimização Avançada para ESP32 (Gzip)

Se você for gravar o modelo na memória física do ESP32:

1. Compacte o arquivo gerado usando gzip no terminal:
   ```bash
   gzip -k -9 modelos/seu_objeto.glb
   ```
   Isso criará `modelos/seu_objeto.glb.gz`.
2. O servidor HTTP do ESP32 (`main.cpp`) entregará automaticamente a versão comprimida `.gz` com o cabeçalho `Content-Encoding: gzip`, economizando até 65% de memória flash!

